# MetalLB install

MetalLB is a loadbalancer for a k8s cluster. These deployment files will use the _metallb-system_ by default.

## Deploy metallb into a cluster

```bash
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.8.1/manifests/metallb.yaml
```


## Configure

Create a config file: metallb_config.yaml and allocate one or more IPs for the cluster loadbalancer.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: custom-ip-space
      protocol: layer2
      addresses:
      - 192.168.39.50-192.168.39.100
```

### Load the config:

```bash
kubectl apply -f metallb_config.yaml
```

## References

[MetalLB](https://metallb.universe.tf/) official site

