# Redis HA

Redis works well with ISIO, just enable injection before deploying redis.

The Redis HA helm chart does not work with less than 2 replicas. Don't use this one for minikube.

## Install redis from helm chart
```bash
helm install stable/redis-ha --name redis --namespace my-app --set replicas=2
```

## Increase replicas

```bash
helm upgrade redis stable/redis-ha --set replicas=3
```

## Istio considerations

When installing into a Istio controlled namespace you may need to set the security context to run as root for the init runner to work. This is not needed if you're using the cni plugin for istio (not currently on by default)

### Enable ISIO for namespace
```bash
kubectl label namespace my-app istio-injection=enabled
```

```bash
helm install stable/redis-ha --name redis --namespace my-app --set replicas=2 \
     --set securityContext.runAsUser=0 --set securityContext.runAsNonRoot=false
```

# Redis (simple)

```bash
helm install stable/redis --name redis --namespace my-app
```

