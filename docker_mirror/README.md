# Setup a local docker mirror

```bash
sudo mkdir /data
sudo cp config.yml /data/config.yml

docker run -d \
    --name docker-mirror \
    --restart unless-stopped \
    -v /data:/var/lib/registry \
    -v /data/config.yml:/etc/docker/registry/config.yml \
    -p 5555:5000 \
    registry:2
```
