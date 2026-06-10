# Monitoring

The monitoring layer runs on a dedicated server and collects metrics and logs from the Kubernetes cluster and supporting infrastructure.

## Services

- Prometheus
- Grafana
- Alertmanager
- Loki
- Promtail
- Node Exporter

## Directory Structure

```bash
mkdir -p /opt/monitoring
cd /opt/monitoring
mkdir prometheus grafana alertmanager loki promtail
```

## Prometheus Targets

```yaml
- 10.90.90.3:9100
- 10.90.90.4:9100
- 10.90.90.5:9100
- 10.90.90.6:9100
- 10.90.90.7:9100
- 10.90.90.8:9100
- 10.90.90.9:9100
```

## Start Stack

```bash
docker compose up -d
docker ps
```

## Validation

```bash
curl -I http://localhost:3000
ip addr
hostname -I
ufw status
ss -tulpn | grep 3000
```

## Dashboard Targets

Recommended dashboard screenshots for the final portfolio version:

- Grafana infrastructure dashboard
- Prometheus targets page
- Kubernetes node metrics
- Harbor registry status
- GitLab Runner status
