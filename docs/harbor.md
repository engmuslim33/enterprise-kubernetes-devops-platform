# Harbor Registry

Harbor is used as the private container registry for the Kubernetes lab.

## Hostname

```text
harbor.lab.local
```

## Project

```text
homelab
```

## Example Image

```text
harbor.lab.local/homelab/nginx:v1
```

## Harbor Operations

```bash
cd /opt/harbor/harbor
./install.sh
docker compose up -d
docker compose ps
docker login harbor.lab.local
```

## Containerd Registry Configuration

Worker nodes were configured to pull from the local Harbor registry using containerd registry host configuration.

```toml
server = "http://harbor.lab.local"

[host."http://harbor.lab.local"]
  capabilities = ["pull", "resolve"]
  skip_verify = true
```

## Pull Validation

```bash
ctr -n k8s.io images pull --plain-http harbor.lab.local/homelab/nginx:v1
crictl pull harbor.lab.local/homelab/nginx:v1
```
