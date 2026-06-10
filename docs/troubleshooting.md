# Troubleshooting

This page documents important troubleshooting areas from the lab. It is intentionally written as a portfolio artifact because real troubleshooting is often more valuable than a clean install guide.

## Harbor DNS Resolution

### Symptom

Kubernetes worker nodes cannot resolve `harbor.lab.local`.

### Checks

```bash
getent hosts harbor.lab.local
cat /etc/hosts
```

### Resolution

Add or correct the local DNS/hosts entry for Harbor:

```text
10.90.90.8 harbor.lab.local
```

## Harbor Image Pull Errors

### Symptom

Pods fail with image pull errors when using images from Harbor.

### Checks

```bash
ctr -n k8s.io images pull --plain-http harbor.lab.local/homelab/nginx:v1
crictl pull harbor.lab.local/homelab/nginx:v1
```

### Resolution

Verify containerd registry configuration under:

```text
/etc/containerd/certs.d/harbor.lab.local/hosts.toml
```

## Containerd Registry Configuration

### Check config path

```bash
grep -n "config_path" /etc/containerd/config.toml
sed -n '45,65p' /etc/containerd/config.toml
```

Expected config path example:

```toml
config_path = '/etc/containerd/certs.d:/etc/docker/certs.d'
```

## Metrics Server Issues

### Symptom

Kubernetes metrics API is unavailable.

### Checks

```bash
kubectl get apiservices | grep metrics
kubectl logs -n kube-system deployment/metrics-server --tail=50
```

### Lab Resolution

Add the following argument to the metrics-server deployment when required by lab TLS conditions:

```yaml
- --kubelet-insecure-tls
```

## GitLab Runner Registration

### Security Note

Never publish GitLab Runner registration tokens, root passwords or access tokens in public repositories.

### Sanitized Registration Flow

```bash
docker exec -it gitlab-runner gitlab-runner register
```

Use placeholders in documentation:

```text
URL: http://10.90.90.7
Token: <GITLAB_RUNNER_REGISTRATION_TOKEN>
Runner Name: HUE-Runner
Tags: docker,k8s
Executor: docker
Default Image: docker:latest
```

## Grafana Datasource Errors

### Checks

- Confirm Prometheus container is running
- Confirm Prometheus targets are up
- Confirm Grafana can reach Prometheus by service name or IP
- Confirm firewall rules allow required ports

```bash
docker ps
curl -I http://localhost:3000
ss -tulpn | grep 3000
```
