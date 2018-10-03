---
title: Kubernetes
taxonomy:
    category:
        - DevOps
---

[TOC]
## Installation on a "bare metal" single Node

There are quite a lot of options [how to install a kubernetes cluster](https://kubernetes.io/docs/setup/pick-right-solution/). 

### Rancher

Since version 2.0 Rancher supports out of the box "production ready" [Kubernetes cluster functionality](https://rancher.com/kubernetes/). The setup is straight forward and is completly dockerized. Just deploy a recent rancher via docker, login to the web UI and from their deploy your kubernetes cluster. Under the hood a original not modified Kubernetes is running. You can either control it via Ranchers UI or with kubectl.

### Kubeadm

[kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) is a toolkit for easy installation of Kubernetes.
After `kube init` the process blocks at `This might take a minute or longer if the control plane images have to be pulled`. Further investigations resulted in the etcd container not starting because of `tcdmain: listen tcp xxx.xxx.xxx.xxx:xxxxx bind: cannot assign requested address`.  To solve this issue create a file `kubeadm.yml`:
```yaml
apiVersion: kubeadm.k8s.io/v1alpha1
kind: MasterConfiguration
etcd:
  extraArgs:
    'listen-peer-urls': 'http://127.0.0.1:2380'
```
and start initialization again with `kubeadm init --config kubeadm.yml`. (see [Github](https://github.com/kubernetes/kubernetes/issues/57709) for details and origin). A previous attempt must be reverted with `kubeadm reset`.

! Be aware that depending on the pod network additional flags for init are required

For example add the following lines to kubeadm.yml for using [Canal](https://github.com/projectcalico/canal/tree/master/k8s-install) pod network

```yaml
kubeProxy:
  config:
    clusterCIDR: "10.244.0.0/16"
```

Check the status with `kubectl get pods --all-namespaces`. If your canal pod is in the status 'CrashLoopBackOff' check the following:
* `kubectl logs canal-zhzph --namespace=kube-system` (adjust pod name)
* check `docker ps -a` for any exiting "flannel" containers and its log with `docker logs CONTAINERID`

Maybe you see messages linke `Error from server (BadRequest): a container name must be specified for pod canal-zhzph, choose one of: [calico-node install-cni kube-flannel]` or `Error registering network: failed to acquire lease: node "HOSTNAME" pod cidr not assigned` than edit `/etc/kubernetes/manifests/kube-controller-manager.yaml` and add to the `command` section
```yaml
    - --allocate-node-cidrs=true
    - --cluster-cidr=10.244.0.0/16
```
Then restart kubelet with `systemctl restart kubelet` ([original hint on Github](https://github.com/coreos/flannel/issues/728)

### Minikube

Minikube is a tool to provision a Kubernetes cluster on a dev box by deploying a Linux virtual machine with e.g. VirtualBox or VMware.

## Kubectl

Get logs of pod
```bash
kubectl logs POD --namespace=NAME
```