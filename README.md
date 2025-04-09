# BestBuy-on-Steroids

A cloud-native e-commerce demo app for Best Buy, powered by microservices, Kubernetes, AI, and Azure services.

---

## 📖 Table of Contents

- [BestBuy-on-Steroids](#bestbuy-on-steroids)
  - [📖 Table of Contents](#-table-of-contents)
  - [🚀 Overview](#-overview)
  - [🧠 Application Architecture](#-application-architecture)
  - [🔍 Service Descriptions](#-service-descriptions)
  - [🛠️ Technology Stack](#️-technology-stack)
  - [⚙️ Deployment Guide](#️-deployment-guide)
  - [📁 Microservice Repositories](#-microservice-repositories)
  - [🐳 Docker Images](#-docker-images)
  - [🎥 Demo Video](#-demo-video)
  - [⚠️ Known Issues or Limitations](#️-known-issues-or-limitations)
  - [🌟 Bonus: CI/CD Integration](#-bonus-cicd-integration)
  - [📚 Resources](#-resources)

---

## 🚀 Overview

BestBuy-on-Steroids is a cloud-native microservices-based e-commerce application built to simulate Best Buy’s online store. It features AI-generated product descriptions and images, asynchronous order processing using Azure Service Bus, and full deployment in a Kubernetes environment.

---

## 🧠 Application Architecture

![Architecture Diagram](./assets/bestbuy-architecture.png)

The architecture is inspired by the "Algonquin Pet Store (On Steroids)" and extended with AI capabilities and a managed message queue. Each component is containerized and deployed to a Kubernetes cluster.

---

## 🔍 Service Descriptions

| Service           | Description                                                               |
|------------------|---------------------------------------------------------------------------|
| **Store-Front**   | Customer-facing UI for browsing products and placing orders              |
| **Store-Admin**   | Admin dashboard for managing products and reviewing order status         |
| **Product-Service** | Handles CRUD operations for product data, stores in MongoDB             |
| **Order-Service** | Receives and processes orders, sends them to Azure Service Bus queue     |
| **Makeline-Service** | Listens to queue and completes order fulfillment                      |
| **AI-Service**    | Uses GPT-4 and DALL·E to generate product descriptions and images         |
| **MongoDB**       | Stores order and product data using Kubernetes StatefulSet               |

---

## 🛠️ Technology Stack

- **Frontend**: Vue
- **Backend**: Node.js / Rust / Go / Python
- **Messaging**: Azure Service Bus
- **AI Integration**: OpenAI (GPT-4 + DALL·E)
- **Database**: MongoDB
- **Containerization**: Docker
- **Orchestration**: Kubernetes (AKS)
- **Secrets & Configs**: Kubernetes Secrets / ConfigMaps

---

## ⚙️ Deployment Guide

1. Clone all microservice repositories.

2. Build and push Docker images:
   ```bash
   docker build -t <dockerhub-user>/store-front ./store-front
   docker push <dockerhub-user>/store-front
   ```
   *(Repeat for all other services)*

3. Create Azure Service Bus namespace and queue:
   ```bash
   az servicebus namespace create --name bestbuy-ns --resource-group myResourceGroup --location eastus
   az servicebus queue create --name orders-queue --namespace-name bestbuy-ns --resource-group myResourceGroup
   ```

4. Create required Kubernetes Secrets:
   ```bash
   kubectl create secret generic openai-secret \
     --from-literal=API_KEY=<your-openai-key>

   kubectl create secret generic azure-bus-secret \
     --from-literal=CONNECTION_STRING=<your-service-bus-connection-string>
   ```

5. Apply Kubernetes manifests to deploy all components:
   ```bash
   kubectl apply -f Deployment-Files/
   ```

6. Access the frontend:
   - If using **NodePort**: open your browser at `http://<node-ip>:<nodeport>`
   - If using **Ingress**: ensure Ingress controller is installed and configured properly

---

## 📁 Microservice Repositories

| Service           | GitHub Repository                             |
|------------------|------------------------------------------------|
| Store-Front       | https://github.com/yourname/store-front        |
| Store-Admin       | https://github.com/yourname/store-admin        |
| Product-Service   | https://github.com/yourname/product-service    |
| Order-Service     | https://github.com/yourname/order-service      |
| Makeline-Service  | https://github.com/yourname/makeline-service   |
| AI-Service        | https://github.com/yourname/ai-service         |

---

## 🐳 Docker Images

| Service           | Docker Image Link                              |
|------------------|-------------------------------------------------|
| Store-Front       | https://hub.docker.com/r/yourname/store-front   |
| Store-Admin       | https://hub.docker.com/r/yourname/store-admin   |
| Product-Service   | https://hub.docker.com/r/yourname/product-service |
| Order-Service     | https://hub.docker.com/r/yourname/order-service |
| Makeline-Service  | https://hub.docker.com/r/yourname/makeline-service |
| AI-Service        | https://hub.docker.com/r/yourname/ai-service    |

---

## 🎥 Demo Video

Watch a demo of the deployed application:

📺 [Click here to watch the demo video](https://youtube.com/your-video-link)

---

## ⚠️ Known Issues or Limitations

- AI-Service may be affected by OpenAI rate limits or latency.
- Admin UI not fully optimized for mobile devices.
- Order-Service assumes Azure Service Bus is always available.

---

## 🌟 Bonus: CI/CD Integration

CI/CD pipelines are implemented using GitHub Actions. Each microservice:
- Builds and pushes Docker images to Docker Hub on commit
- Triggers a rolling update in Kubernetes cluster

Example `.github/workflows/deploy.yml` is included in each repository.

---

## 📚 Resources

- [Algonquin Pet Store (On Steroids)](https://github.com/ramymohamed10/algonquin-pet-store-on-steroids)
- [Azure Service Bus Documentation](https://learn.microsoft.com/en-us/azure/service-bus-messaging/)
- [OpenAI API Docs](https://platform.openai.com/docs/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
```

