# Installing vitess

```bash
mkdir -p ~/Dev/k8s/vitess
cd ~/Dev/k8s/vitess
kubectl create namespace vitess
kubens vitess
```

## Install etcd operator
```bash
cd ~/Dev/k8s/vitess
git clone https://github.com/coreos/etcd-operator.git
cd etcd-operator
git pull
NAMESPACE=vitess example/rbac/create_role.sh
kubectl create -f example/deployment.yaml
```

## Install vitess
```bash
cd ~/Dev/k8s/vitess
git clone https://github.com/vitessio/vitess.git
cd vitess
git pull
```

### Create values file:
This file is for the *rpi* database (keyspace):
```yaml
topology:
  cells:
    - name: "zone1"
      etcd:
        replicas: 1
      vtctld:
        replicas: 1
      vtgate:
        replicas: 1
      mysqlProtocol:
        enabled: true
        #authType: "none"
        authType: secret
        username: rpi
        # kubectl create secret generic rpi-db-password --from-literal=password=rpi123
        passwordSecret: rpi-db-password
      keyspaces:
        - name: "rpi"
          shards:
            - name: "0"
              tablets:
                - type: "replica"
                  vttablet:
                    replicas: 1
```

```bash
kubectl create secret generic rpi-db-password --from-literal=password=rpi123
helm install helm/vitess --namespace vitess --name vitess -f ../values.yaml
```

## References

- [etcd-operator](https://github.com/coreos/etcd-operator/blob/master/doc/user/install_guide.md)
- [vitess install](https://vitess.io/docs/tutorials/kubernetes/)

