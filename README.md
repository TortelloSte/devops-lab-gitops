# DevOps GitOps Lab

A local Kubernetes platform engineering lab built to explore GitOps, observability, security, secrets management and Kubernetes operations.

## Architecture

The environment runs on a 3-node Kubernetes cluster created with kind.

```text
GitHub
  │
  │ Git
  ▼
Argo CD
  │
  │ Continuous reconciliation
  ▼
Kubernetes
├── demo application
├── ingress-nginx
├── metrics-server
├── Prometheus
├── Grafana
├── Alertmanager
├── Loki
├── Grafana Alloy
├── External Secrets Operator
└── Kyverno
```

## Stack

- Kubernetes
- kind
- Docker
- Argo CD
- ingress-nginx
- Helm
- Prometheus
- Grafana
- Alertmanager
- Loki
- Grafana Alloy
- External Secrets Operator
- Kyverno
- SOPS
- age
- Trivy
- Cosign
- OpenTofu
- Ansible
- AWS CLI

## GitOps Workflow

Application state is stored in Git and continuously reconciled by Argo CD.

```text
Developer
    │
    ▼
Git commit / push
    │
    ▼
GitHub repository
    │
    ▼
Argo CD
    │
    ▼
Kubernetes cluster
```

Argo CD is configured with:

- automated synchronization
- self-healing
- automatic pruning
- automatic namespace creation

Manual changes made directly to Kubernetes are therefore reconciled back to the desired state stored in Git.

## Demo Application

The example application is deployed in the `demo` namespace.

Files:

```text
apps/demo/
├── deployment.yaml
├── ingress.yaml
└── service.yaml
```

The application is exposed locally through:

```text
http://demo.local
```

Traffic flow:

```text
demo.local
    │
    ▼
localhost:80
    │
    ▼
kind control-plane
    │
    ▼
ingress-nginx
    │
    ▼
Kubernetes Service
    │
    ▼
Application Pods
```

## Observability

The cluster includes:

- Prometheus for metrics collection
- Grafana for visualization
- Alertmanager for alerts
- metrics-server for Kubernetes resource metrics
- Loki for log storage and querying
- Grafana Alloy for log collection

## Security

The lab includes:

- Kyverno for Kubernetes policy management
- Trivy for vulnerability scanning
- Cosign for container signing
- SOPS + age for encrypted secrets
- External Secrets Operator for external secret integration

## Repository Structure

```text
.
├── apps/
│   └── demo/
├── argocd/
│   └── apps/
├── clusters/
│   └── local/
├── docs/
└── README.md
```

## Status

The current environment runs a three-node Kubernetes cluster with GitOps, ingress, metrics, monitoring, centralized logging, secrets management and policy tooling.

This repository is intended as a hands-on Platform Engineering / DevOps lab and will be expanded with CI/CD, infrastructure as code and cloud deployment.
