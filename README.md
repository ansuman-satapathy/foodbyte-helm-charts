# FoodByte Helm Charts

This repository serves as the central template library for the FoodByte microservices ecosystem. It contains the modular Helm charts used to package and configure each service for both local development and production.

## Chart Design Principles
The charts follow a "Hybrid" model, allowing them to adapt to different environments without code changes:

- Service Logic: Standard Kubernetes Deployments for application containers.
- Stateful Logic: Self-hosted databases (PostgreSQL, MongoDB, Redis, RabbitMQ) managed as StatefulSets.
- Persistence: Automated PersistentVolumeClaims (PVCs) ensure data durability.
- Portability: Configurable via values-prod.yaml to switch between local development and AWS production settings (e.g., EBS StorageClasses and GHCR pull secrets).

## Repository Structure
Each directory represents a standalone Helm chart:
- foodbyte-user-service: PostgreSQL + FastAPI.
- foodbyte-order-service: PostgreSQL + FastAPI + RabbitMQ.
- foodbyte-restaurant-service: MongoDB + FastAPI.
- foodbyte-notification-service: Redis + RabbitMQ + FastAPI.
- foodbyte-frontend: React (Vite) + Nginx.

## Integration
- Local Development: Tilt (via the root Tiltfile) uses these charts to build and sync code in real-time.
- Cloud Deployment: The foodbyte-gitops repository references these charts to maintain the desired state of the production cluster.
