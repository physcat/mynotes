# Kubernetes setup

When creating a k8s cluster here are some tasks to consider (in order)

- Create a docker registry [mirror](docker-mirror.md)
- Configure each node to use the mirror
- Create the cluster
- Configure a Loadbalancer
- Configure Persistant storage
- Install the Service Mesh
- Install applications

## Create a cluster

- [minikube](minikube.md)
- [Rancher](https://rancher.com/docs/rancher/v2.x/en/installation/ha/) using rke


## Loadbalancer

On prem k8s clusters tend not to have load balancers, here we can use [MetalLB](metallb.md)


## Persistant storage:

Minikube has some basic persistant storage but other on prem solutions do not.

- Rook/Ceph

## Service Mesh

- [ISTIO](istio.md)

## DataBases

- [Redis](redis.md)
- [Vitess](vitess.md)

