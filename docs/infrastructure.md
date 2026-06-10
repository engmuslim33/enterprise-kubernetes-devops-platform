# Infrastructure

## Virtual Machines

| VM | Role | IP Address | Main Services |
| --- | --- | --- | --- |
| VM-01 | Kubernetes Master | 10.90.90.3 | kubectl, Helm, MetalLB, Ingress, metrics components |
| VM-02 | Worker01 | 10.90.90.4 | containerd, Kubernetes workloads |
| VM-03 | Worker02 | 10.90.90.5 | containerd, Kubernetes workloads |
| VM-04 | Harbor | 10.90.90.8 | Harbor Registry, Docker Compose |
| VM-05 | GitLab | 10.90.90.7 | GitLab CE, GitLab Runner |
| VM-06 | Monitoring | 10.90.90.9 | Prometheus, Grafana, Alertmanager, Loki, Promtail, Node Exporter |

## DNS Entries

```text
10.90.90.7   gitlab.lab.local
10.90.90.8   harbor.lab.local
10.90.90.9   grafana.lab.local
```

## MetalLB Address Pool

```text
10.90.90.100-10.90.90.120
```

## Example Validation Commands

```bash
kubectl get nodes
kubectl get pods -A
kubectl get svc
kubectl get svc -n ingress-nginx
kubectl get pods -n metallb-system -o wide
kubectl get apiservices | grep metrics
```
