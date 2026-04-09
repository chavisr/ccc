# CLAUDE.md - Kubernetes Manifest Project Example

This is an example CLAUDE.md file for a Kubernetes project using Kustomize.

## Project Purpose

Kubernetes manifests for application deployment across dev, staging, and production environments using Kustomize overlays.

## Repository Structure

```
my-app/
├── k8s/
│   ├── base/
│   │   ├── kustomization.yaml
│   │   ├── deployment.yaml
│   │   ├── service.yaml
│   │   ├── configmap.yaml
│   │   └── ingress.yaml
│   ├── dev/
│   │   ├── kustomization.yaml
│   │   └── patches/
│   ├── staging/
│   │   ├── kustomization.yaml
│   │   └── patches/
│   └── production/
│       ├── kustomization.yaml
│       └── patches/
├── src/                     # Application source code
└── CLAUDE.md                # This file
```

## This Project

### Application

- Name: [APP_NAME]
- Image: [REGISTRY/IMAGE:TAG - e.g., docker.io/myorg/myapp:1.0.0]
- Port: [PORT - e.g., 8080]
- Health check path: [PATH - e.g., /healthz]

### Resources per Environment

| Setting | Dev | Staging | Production |
|---------|-----|---------|------------|
| Replicas | 1 | 2 | 3 |
| CPU request | 100m | 250m | 500m |
| Memory request | 128Mi | 256Mi | 512Mi |
| HPA | No | No | Yes (2-10) |

### Networking

- Service type: ClusterIP
- Ingress hosts:
  - Dev: [APP_NAME].dev.example.com
  - Staging: [APP_NAME].staging.example.com
  - Production: [APP_NAME].example.com
- TLS: Production only

### Configuration

- ConfigMap keys: [KEY1, KEY2, ...]
- Secrets needed: [SECRET_NAME1, SECRET_NAME2, ...]

## When Working on This

Use the `kube-manifest` agent to create and modify Kubernetes manifests.

**Example prompt:**
```
Create the manifests
```

Claude will read this CLAUDE.md file and have all the details needed.
