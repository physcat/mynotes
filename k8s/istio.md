# Istio

## On minikube

```bash
curl -L https://git.io/getLatestIstio | sh -
cd istio-1.1.2
for i in install/kubernetes/helm/istio-init/files/crd*yaml; do kubectl apply -f $i; done
kubectl apply -f install/kubernetes/istio-demo.yaml
```


## Using helm
### Install with cni plugin
```bash
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.1.2/charts/
helm update
kubectl create namespace istio-system
helm install istio.io/istio-init --name istio-init --namespace istio-system --set istio_cni.enabled=true
helm install istio.io/istio-cni --name=istio-cni --namespace=istio-system
helm install istio.io/istio --name istio --namespace istio-system \
     --set istio_cni.enabled=true \
     --set tracing.enabled=true \
     --set tracing.ingress.enabled=true \
     --set kiali.enabled=true \
     --set kiali.ingress.hosts='' \
     --set kiali.ingress.enabled=true \
     --set grafana.enabled=true \
     --set grafana.ingress.hosts=''
     
```
On GKE clusters you need to enable "Network policy" and change the istio bin path used for cni
```bash
helm install istio.io/istio-cni --name=istio-cni --namespace=istio-system --set cniBinDir=/home/kubernetes/bin
```

### Install without cni plugin
```bash
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.1.2/charts/
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

