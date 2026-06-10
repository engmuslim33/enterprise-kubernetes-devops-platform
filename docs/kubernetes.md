# Kubernetes

This section documents the Kubernetes components used in the lab.

## Installed Components

- Helm
- MetalLB
- NGINX Ingress
- Metrics Server
- Kube State Metrics
- NGINX test workloads
- Harbor-backed Kubernetes workload images

## Helm

```bash
curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm repo add metallb https://metallb.github.io/metallb
helm repo update
```

## MetalLB Installation

```bash
helm install metallb metallb/metallb \
  -n metallb-system \
  --create-namespace
```

## Metrics Server

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
kubectl edit deployment metrics-server -n kube-system
```

For this lab environment, the following argument was added:

```yaml
- --kubelet-insecure-tls
```

## Kube State Metrics

```bash
kubectl apply -f https://github.com/kubernetes/kube-state-metrics/releases/latest/download/standard.yaml
```

## Useful Operations

```bash
kubectl get pods -A
kubectl get pods -o wide
kubectl get svc
kubectl get svc -n ingress-nginx
kubectl logs -n kube-system deployment/metrics-server --tail=50
```
