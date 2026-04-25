# FoodByte Orchestration 📦

This is the central repository for the FoodByte microservices ecosystem. It contains the **production-grade Helm charts**, Gateway API configurations, and automation logic used to deploy and manage the entire stack—from a local developer's machine to a production cluster on AWS EKS.

## 🏗️ Architecture
FoodByte is built on a modular microservices architecture, with each service packaged as an independent Helm chart:
- `foodbyte-frontend`: React (Vite) + Nginx
- `foodbyte-user-service`: FastAPI + PostgreSQL
- `foodbyte-restaurant-service`: FastAPI + MongoDB
- `foodbyte-order-service`: FastAPI + PostgreSQL + RabbitMQ
- `foodbyte-notification-service`: FastAPI + Redis + RabbitMQ

## 🌐 Modern Networking
The ecosystem uses the **Kubernetes Gateway API** with **Envoy Gateway**. 
- All routing rules are consolidated in a "Master Route" (`gateway.yaml`) to ensure deterministic path priority and prevent traffic shadowing.

## ⚡ Unified Development Loop
I believe the development environment should be as robust as production. I use **Tilt** and **Kind** to provide a "One-Click" setup for the entire stack.
- **Instant Feedback**: Every code change in a service repository triggers an automatic container rebuild and pod roll-out.
- **Infrastructure Safety**: All services utilize `initContainers` to ensure TCP readiness for databases and message brokers before the application starts.

## 🚀 Deployment Strategy
1. **Local**: Automated via `tilt up` and `kind`.
2. **Cloud**: Provisioned via **Terraform** on AWS (VPC, EKS, RDS, DocumentDB).
3. **Continuous Delivery**: Managed via **Flux CD** (GitOps), using this repository as the source of truth for the cluster state.


## 🛠️ Quick Start (Local)
1. **Cluster Setup**: `kind create cluster --config kind-config.yaml`
2. **Launch Stack**: `tilt up`
3. **Access App**: `http://localhost:8000`

