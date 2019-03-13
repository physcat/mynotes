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

## Point to local docker registry mirror

```
IP=$(ip route get 1 | sed 's/^.*src \([0-9.]*\).*/\1/' |head -1)
minikube start --registry-mirror http://${IP}:5555
```

