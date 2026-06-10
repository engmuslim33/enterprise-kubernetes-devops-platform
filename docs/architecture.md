# Architecture

The lab is designed as a complete self-hosted DevOps platform. It separates source control, registry, Kubernetes workloads and monitoring into dedicated virtual machines.

## Logical Flow

1. Developers push application code to GitLab CE.
2. GitLab Runner executes CI/CD jobs.
3. Built container images are pushed to Harbor Registry.
4. Kubernetes worker nodes pull images from Harbor through containerd.
5. Applications are deployed to the Kubernetes cluster.
6. MetalLB provides LoadBalancer IP addresses for services.
7. NGINX Ingress routes HTTP traffic to applications.
8. Prometheus, Grafana, Loki and Alertmanager monitor platform health.

## Network Design

| Service | Address |
| --- | --- |
| GitLab | gitlab.lab.local / 10.90.90.7 |
| Harbor | harbor.lab.local / 10.90.90.8 |
| Grafana | grafana.lab.local / 10.90.90.9 |
| MetalLB Pool | 10.90.90.100-10.90.90.120 |

## Platform Layers

| Layer | Components |
| --- | --- |
| Source Control | GitLab CE |
| CI/CD | GitLab Runner |
| Registry | Harbor |
| Orchestration | Kubernetes, containerd |
| Networking | MetalLB, NGINX Ingress |
| Observability | Prometheus, Grafana, Loki, Promtail, Alertmanager, Node Exporter |
| Administration | Linux, Docker, shell scripting, kubectl, Helm |
