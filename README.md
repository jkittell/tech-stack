# k8s-gitops

GitOps repository for managing Kubernetes clusters.

# Development Tech Stack

A complete development platform using Kubernetes (MicroK8s) with integrated services for database management, monitoring, and search capabilities.

## Components

- **Database Layer**
  - CrateDB: Vector database and structured data storage
  - KeyDB: High-performance Redis-compatible cache

- **Storage**
  - MinIO: S3-compatible object storage

- **Monitoring**
  - Prometheus: Metrics collection and alerting
  - Grafana: Metrics visualization and dashboards

- **Search**
  - SearXNG: Privacy-respecting metasearch engine

## Quick Start

1. Install MicroK8s:
```bash
snap install microk8s --classic
microk8s enable dns storage helm3 metallb ingress
```

2. Clone and deploy:
```bash
git clone https://github.com/jkittell/tech-stack.git
cd tech-stack
flux bootstrap github \
  --owner=jkittell \
  --repository=tech-stack \
  --branch=main \
  --path=./clusters/cloud \
  --personal
```

3. Access Services:
- CrateDB: http://${DOMAIN}/cratedb
- Grafana: http://${DOMAIN}/grafana
- MinIO Console: http://${DOMAIN}/minio-console
- Search: http://${DOMAIN}/search

## Development

This stack can be run locally or in the cloud. For development:
- Local: Use `clusters/local` configuration
- Cloud: Use `clusters/cloud` configuration

## Cost Management

The stack can be scaled to zero when not in use:
1. Take snapshot of droplet
2. Power off droplet
3. Only pay for snapshot storage (~$4/month)
4. Power on when needed (~$0.07/hour)
