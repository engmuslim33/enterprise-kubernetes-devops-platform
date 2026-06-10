# Lessons Learned

## Platform Design

Building the platform across multiple virtual machines made the environment closer to a real enterprise setup than a single-machine demo. Separating GitLab, Harbor, Kubernetes and monitoring helped clarify service boundaries and troubleshooting paths.

## Kubernetes Networking

MetalLB is useful for exposing LoadBalancer services in a bare-metal or homelab environment. NGINX Ingress provides a clean HTTP routing layer above Kubernetes services.

## Registry Integration

Harbor integration requires both DNS resolution and containerd registry configuration on worker nodes. Image pull issues are easier to troubleshoot by testing with `ctr` and `crictl` before debugging Kubernetes workloads.

## Observability

Prometheus, Grafana, Loki and Node Exporter provide visibility into host and platform health. Monitoring is more useful when documented together with validation commands and screenshots.

## Security

Public documentation should never include tokens, root passwords, GitLab Runner registration tokens or private credentials. Use placeholders for sensitive values and rotate any secret that was accidentally exposed during lab work.
