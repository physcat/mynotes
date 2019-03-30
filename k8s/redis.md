# Install redis from helm chart

```bash
helm install stable/redis-ha --name redis --namespace rpi --set replicas=1
```

## Increase replicas

```bash
helm upgrade redis stable/redis-ha --set replicas=2
```
