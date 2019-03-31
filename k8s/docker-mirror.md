# Docker Mirror


This discribes running a local docker container using a local path to mirror/proxy docker.io

### Local path for files and config

```bash
sudo mkdir /data
```

Create _config.yml_

```yaml
version: 0.1
log:
  fields:
    service: registry
storage:
  cache:
    blobdescriptor: inmemory
  filesystem:
    rootdirectory: /var/lib/registry
http:
  addr: :5000
  headers:
    X-Content-Type-Options: [nosniff]
proxy:
  remoteurl: https://registry-1.docker.io
health:
  storagedriver:
    enabled: true
    interval: 10s
    threshold: 3
```

```bash
sudo cp config.yml /data/config.yml
```

### Start docker container

```bash
docker run -d \
    --name docker-mirror \
    --restart unless-stopped \
    -v /data:/var/lib/registry \
    -v /data/config.yml:/etc/docker/registry/config.yml \
    -p 5000:5000 \
    registry:2
```
