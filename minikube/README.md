# Minikube setup

## Config

```bash
mkdir -p ~/.minikube/config/
cp config.json ~/.minikube/config/
```


## start minikube

```bash
minikube start
```

## Start with local docker registry mirror

```
IP=$(ip route get 1 | sed 's/^.*src \([0-9.]*\).*/\1/' |head -1)
minikube start --registry-mirror http://${IP}:5555
```

## Configure metallb

```bash
kubectl apply -f https://raw.githubusercontent.com/google/metallb/v0.7.3/manifests/metallb.yaml
kubectl apply -f metallb_config.yaml
```

## install istio

```bash
curl -L https://git.io/getLatestIstio | sh -
cd istio-1.0.6
kubectl apply -f install/kubernetes/helm/istio/templates/crds.yaml
￼kubectl apply -f install/kubernetes/istio-demo.yaml
￼```

