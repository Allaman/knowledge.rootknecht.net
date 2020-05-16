---
title: Kubernetes
taxonomy:
    category:
        - Linux
        - DevOps
---

[TOC]

## Tools and workflow


## Scaling deployment deletion sequence

Pod deletion preference is based on a ordered series of checks, defined in code here:
https://github.com/kubernetes/kubernetes/blob/release-1.11/pkg/controller/controller_utils.go#L737

Summarizing- precedence is given to delete pods:

* that are unassigned to a node, vs assigned to a node
* that are in pending or not running state, vs running
* that are in not-ready, vs ready
* that have been in ready state for fewer seconds
* that have higher restart counts
* that have newer vs older creation times
* These checks are not directly configurable.

<small>[origin](https://stackoverflow.com/a/51471388)</small>

## Check permission of service accounts
```sh
kubectl auth can-i list deployment --as=system:serviceaccount:default:<NAME> -n <NAME>
```

## Run a quick pod for testing

```sh
kubectl run test -n NAMESPACE --rm -i --tty --image debian -- bash
```

## Get kubeconfig via AWS cli

```sh
aws --profile=<AWS PROFILE> eks update-kubeconfig --name <CLUSTER NAME>
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
