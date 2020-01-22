
# Set up a Kubernetes cluster

## General
[Kind](https://github.com/kubernetes-sigs/kind) will be used as the k8s runtime environment as it can easily run on all environments, and does not require any complicated steps to setup.

## Install Kind

See: [installing Kind](https://kind.sigs.k8s.io/docs/user/quick-start/)

## Create Kind Demo Cluster

Use kind to create the customized cluster:

```console
kind create cluster --config=env/cluster.yaml --name=octarine-workshop --image=docker.io/kindest/node:v1.16.3@sha256:70ce6ce09bee5c34ab14aec2b84d6edb260473a60638b1b095470a3a0f95ebec
```
NOTE: The latest version of kind and the kind container version can be found [here](https://github.com/kubernetes-sigs/kind/releases)

## Set up the Kubernetes environment 

Install Calico for `NetworkPolicy` support:

```console
kubectl apply -f env/calico.yaml
```

## Verifying the cluster is ready:

```console
kubectl get pods -A
```

Should show:

```console
NAMESPACE     NAME                                         READY   STATUS    RESTARTS   AGE
kube-system   calico-kube-controllers-648f4868b8-8klhf     1/1     Running   0          81s
kube-system   calico-node-c7k54                            1/1     Running   0          81s
kube-system   calico-node-lww2l                            1/1     Running   0          81s
kube-system   coredns-5644d7b6d9-mh2q7                     1/1     Running   0          10m
kube-system   coredns-5644d7b6d9-tjfqr                     1/1     Running   0          10m
kube-system   etcd-demo-control-plane                      1/1     Running   0          9m21s
kube-system   kube-apiserver-demo-control-plane            1/1     Running   0          9m11s
kube-system   kube-controller-manager-demo-control-plane   1/1     Running   0          9m29s
kube-system   kube-proxy-9ztn7                             1/1     Running   0          10m
kube-system   kube-proxy-lcg8x                             1/1     Running   0          9m58s
kube-system   kube-scheduler-demo-control-plane            1/1     Running   0          9m5s
```

## Environment Cleanup 
In order to cleanup the environment you can simply delete the kind cluster by running the fallowing command:

```console
kind delete cluster --name octarine-workshop
```