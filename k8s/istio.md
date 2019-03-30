# Install Istio

## Using helm
### Install with cni plugin
```bash
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.1.1/charts/
helm update
kubectl create namespace istio-system
helm install istio.io/istio-cni --name=istio-cni --namespace=istio-system
helm install istio.io/istio --name istio --namespace istio-system \
     --set istio_cni.enabled=true
```

### Install without cni plugin
```bash
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.1.1/charts/
helm update
kubectl create namespace istio-system
helm install istio.io/istio-init --name istio-init --namespace istio-system
helm install istio.io/istio --name istio --namespace istio-system
```

## Further Reading

- [kiali](https://www.kiali.io/) Service mesh observability

## References

- [github istio](https://github.com/istio/istio)
- [github istio helm](https://github.com/istio/istio/tree/master/install/kubernetes/helm/istio)
- [istio install with cni](https://istio.io/docs/setup/kubernetes/additional-setup/cni/)
- [istio download](https://istio.io/docs/setup/kubernetes/download/)
- [istio helm install](https://istio.io/docs/setup/kubernetes/install/helm/)
