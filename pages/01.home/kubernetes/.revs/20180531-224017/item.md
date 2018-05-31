---
title: Kubernetes
taxonomy:
    category:
        - DevOps
    author:
        - Knecht
---

[TOC]
## Installation on a "bare metal" single Node

There are quite a lot of options [how to install a kubernetes cluster](https://kubernetes.io/docs/setup/pick-right-solution/). 

### Rancher

Since version 2.0 Rancher supports out of the box "production ready" [Kubernetes cluster functionality](https://rancher.com/kubernetes/). The setup is straight forward and is completly dockerized. Just deploy a recent rancher via docker, login to the web UI and from their deploy your kubernetes cluster. Under the hood a original not modified Kubernetes is running. You can either control it via Ranchers UI or with kubectl.

### Kubeadm

[kubeadm](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/) is a toolkit for easy installation of Kubernetes. Follow the [Installation Instructions](https://kubernetes.io/docs/tasks/tools/install-kubeadm/) and the [Usage Instructions](https://kubernetes.io/docs/setup/independent/create-cluster-kubeadm/#instructions).

! Be aware that depending on the pod network additional flags for init are required

For the [Canal](https://github.com/projectcalico/canal/tree/master/k8s-install) pod network use `--pod-network-cidr=10.244.0.0/16`

After initialization execute
```bash
kubectl apply -f https://raw.githubusercontent.com/projectcalico/canal/master/k8s-install/1.7/rbac.yaml
kubectl apply -f https://raw.githubusercontent.com/projectcalico/canal/master/k8s-install/1.7/canal.yaml
```

! When running as a single node cluster turn off master isolation before deploying stuff

#### Troubleshooting:

After `kube init` the process blocks at `This might take a minute or longer if the control plane images have to be pulled`. Further investigations resulted in the etcd container not starting because of `tcdmain: listen tcp xxx.xxx.xxx.xxx:xxxxx bind: cannot assign requested address`.  To solve this issue create a file `kubeadm.yml`:
```yaml
apiVersion: kubeadm.k8s.io/v1alpha1
kind: MasterConfiguration
etcd:
  extraArgs:
    'listen-peer-urls': 'http://127.0.0.1:2380'
```
and start initialization again with `kubeadm init --config kubeadm.yml`. (see [Github](https://github.com/kubernetes/kubernetes/issues/57709) for details and origin). A previous attempt must be reverted with `kubeadm reset`.

Check the status with `kubectl get pods --all-namespaces`. If your canal pod is in the status 'CrashLoopBackOff' check the following:
* `kubectl logs canal-zhzph --namespace=kube-system` (adjust pod name)
* check `docker ps -a` for any exiting "flannel" containers and its log with `docker logs CONTAINERID`

Maybe you see messages linke `Error from server (BadRequest): a container name must be specified for pod canal-zhzph, choose one of: [calico-node install-cni kube-flannel]` or `Error registering network: failed to acquire lease: node "HOSTNAME" pod cidr not assigned` than edit `/etc/kubernetes/manifests/kube-controller-manager.yaml` and add to the `command` section
```yaml
    - --allocate-node-cidrs=true
    - --cluster-cidr=10.244.0.0/16
```
Then restart kubelet with `systemctl restart kubelet` ([original hint on Github](https://github.com/coreos/flannel/issues/728)

DNS warnings can be resolved by editing `/etc/hosts`

### Minikube

Minikube is a tool to provision a Kubernetes cluster on a dev box by deploying a Linux virtual machine with e.g. VirtualBox or VMware.

## Kubectl

Get logs of pod
```bash
kubectl logs POD --namespace=NAME
```

List all pods
```bash
kubectl get pods --all-namespaces
```

List all deployments
```bash
kubectl get deployment --all-namespaces
```

List all services
```bash
kubectl get svc --all-namespaces
```

List all roles
```bash
kubectl get clusterroles
```

## Deploy Dashboard

Deploy dashboard
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```

Start proxy
```bash
kubectl proxy [-p 8080] 
```

Access dashboard http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/ (adjust port if necessary)

Get login token

```bash
kubectl -n kube-system get secret # list service accounts
kubectl -n kube-system describe secret deployment-controller-token-****
```

Alternative grant dashboard admin rights:
Create `dashboard-admin.yml' with following content:
```yaml
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: kubernetes-dashboard
  labels:
    k8s-app: kubernetes-dashboard
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: kubernetes-dashboard
  namespace: kube-system
```
Deploy to your cluster `kubectl create -f dashboard-admin.yml`. Then you skip authentication in the login screen

## helm

[Powerful "package manager" for Kubernetes](https://github.com/kubernetes/helm). Install client for example with your system's package manager. With an already configured kubectl run `helm init` to install on your Kubernetes the server side component named `tiller`. Update helm's repo information with `help repo update`. Inspect a package with `helm inspect`.

When you encounter the error `Error: release jenkins failed: namespaces "dev" is forbidden: User "system:serviceaccount:kube-system:default" cannot get namespaces in the namespace "dev"` during installation of a package execute `kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default` in order to add the role cluster-admin to the serviceaccount kube-system:default.

## Create namespace
```bash
cat <<EOF | kubectl create -f -
{
  "kind": "Namespace",
  "apiVersion": "v1",
  "metadata": {
    "name": "dev",
    "labels": {
      "name": "dev"
    }
  }
}
EOF
```