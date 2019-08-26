# Minikube setup

## Install minikube
```bash
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

Reference: [github](https://github.com/kubernetes/minikube)

## Install minikube KVM2 driver
Follow the official installation instructions on [github](https://github.com/kubernetes/minikube/blob/master/docs/drivers.md#kvm2-driver)


## Configure

By default minikube starts a vm with only 2 CPUs and 2G ram, we want to change some of the defaults.

Create the config file: ~/.minikube/config/config.json
```json
{
    "cpus": 4,
    "dashboard": true,
    "heapster": true,
    "memory": 12000,
    "vm-driver": "kvm2"
}
```

## start minikube

```bash
minikube start
```

Or Start with local docker registry mirror

```bash
IP=$(ip route get 1 | sed 's/^.*src \([0-9.]*\).*/\1/' |head -1)
minikube start --registry-mirror http://${IP}:5555
```


