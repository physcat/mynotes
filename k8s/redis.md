# Install redis from helm chart

```bash
helm install stable/redis-ha --name redis --namespace rpi --set replicas=1
```

## Increase replicas

```bash
helm upgrade redis stable/redis-ha --set replicas=2
```
## Istio

When installing into a Istio controlled namespace you may need to set the security context to run as root for the init runner to work. This is not needed if you're using the cni plugin for istio (not currently on by default)

``bash
helm install stable/redis-ha --name redis --namespace rpi --set replicas=1 \
     --set securityContext.runAsUser=0 --set securityContext.runAsNonRoot=false
```
