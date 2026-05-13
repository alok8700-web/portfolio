# NovaPay Zero-Downtime CI/CD (Simulation)

This repository is an enterprise DevOps architecture simulation for NovaPay Digital Bank.

## Scope
- Java 21 + Spring Boot payment microservice
- GitHub Actions CI pipeline with quality/security gates
- Docker + Kubernetes + Helm + ArgoCD manifests
- Terraform examples, OPA policy examples
- Runbooks, rollback, compliance, and observability docs

## Microservice API
- `GET /health`
- `GET /payments`
- `POST /payments`


## Requirements to run locally
- **Java 21 (JDK)**
- **Maven 3.9+**
- **Docker** (for container build/run)
- **Kubernetes tooling**: `kubectl` and optionally **Minikube**
- **Helm 3** (for chart-based deploy)
- Optional for full pipeline simulation: GitHub Actions, SonarQube server, Trivy, ArgoCD

## Run the application locally (without Kubernetes)
```bash
cd app
mvn clean package
java -jar target/*.jar
```
Then test:
```bash
curl http://localhost:8080/health
curl http://localhost:8080/payments
curl -X POST http://localhost:8080/payments -H "Content-Type: application/json" -d '{"amount":1000}'
```

## Run with Docker
```bash
cd app
docker build -t novapay-app .
docker run --rm -p 8080:8080 novapay-app

# verify
curl http://localhost:8080/health
```

## Run on Kubernetes (Minikube example)
```bash
minikube start
kubectl apply -f ../k8s/deployment.yaml
kubectl apply -f ../k8s/service.yaml
kubectl get pods
kubectl get svc novapay-service
```

## Run with Helm
```bash
helm upgrade --install novapay ../pipeline/helm
kubectl get deploy,pods,svc
```
