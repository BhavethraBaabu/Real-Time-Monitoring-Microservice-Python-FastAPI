# DevOps Observability Demo

A small cloud-native demo showing DevOps practices:

- FastAPI service with `/health`, `/hello`, and `/metrics` endpoints
- Prometheus scraping application metrics
- Grafana ready for dashboards
- Docker and Docker Compose for local development
- Kubernetes manifests for deployment on a cluster (e.g., AWS EKS)
- GitHub Actions CI pipeline that builds and tests the container image and pushes to GitHub Container Registry (GHCR)

## Getting Started

### Prerequisites

- Docker and Docker Compose installed
- Python 3.11+ if you want to run the app directly

### Run with Docker Compose

```bash
docker-compose up --build
```

Services:

- App: http://localhost:8000/health
- Metrics: http://localhost:8000/metrics
- Prometheus: http://localhost:9090
- Grafana: http://localhost:3000

### Kubernetes Manifests

The `k8s/` directory contains sample `Deployment` and `Service` manifests for running the app on a Kubernetes cluster.

Update the image field in `deployment.yaml` to match your container registry:

```yaml
image: ghcr.io/YOUR_GITHUB_USERNAME/devops-observability-demo:latest
```

Then apply:

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
```

### CI Pipeline

GitHub Actions workflow is defined in `.github/workflows/ci.yml`:

- Installs dependencies
- Runs a basic import test
- Builds the Docker image
- Pushes the image to GitHub Container Registry on pushes to `main`
