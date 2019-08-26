#KIND (Kubernetes IN Docker)


## Get Binary
Get the kind binary using go:

```bash
go get sigs.k8s.io/kind
```

Or get the binary from [github](https://github.com/kubernetes-sigs/kind/releases)


## Setup and create cluster

Create a config file: kind-cluster.yaml

```yaml
kind: Cluster
apiVersion: kind.sigs.k8s.io/v1alpha3
nodes:
- role: control-plane
- role: worker
- role: worker
```

Create the cluster:

```bash
kind create cluster --name cluster-1 --config kind_worker.yaml
```

## Use the Cluster

```bash
export KUBECONFIG="$(kind get kubeconfig-path --name="kind")"
kubectl get nodes -o wide
```

## Loadbalancer (optional)

After checking the IPs for the cluster it my be useful to expose a small
range using metallb

```bash
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.8.1/manifests/metallb.yaml
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 172.17.255.1-172.17.255.250
EOF
```


## References

- [kind](https://kind.sigs.k8s.io/docs/user/quick-start/)
- [metallb](https://metallb.universe.tf/installation/)

