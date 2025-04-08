# BestBuy-on-Steroids: Cloud-Native Microservices E-Commerce Application

## Overview

BestBuy-on-Steroids is a cloud-native, full-stack microservices-based e-commerce demo app developed for Best Buy. Inspired by the Algonquin Pet Store (on Steroids) architecture, this application demonstrates modern cloud-native design using Kubernetes, managed messaging services, and AI integration.

---

## Architecture Diagram

![Architecture Diagram](./assets/bestbuy-architecture.png)

---

## 🛠️ Application Functionality

| Service              | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| **Store-Front**      | Frontend for customers to browse products and place orders.                 |
| **Store-Admin**      | Admin dashboard for employees to manage products and view orders.           |
| **Order-Service**    | Handles order creation and sends orders to Azure Service Bus queue.         |
| **Product-Service**  | Provides CRUD APIs for managing product information.                        |
| **Makeline-Service** | Processes orders from the queue and marks them as completed.                |
| **AI-Service**       | Integrates with GPT-4 and DALL·E to generate product descriptions and images. |
| **MongoDB**          | Stores product and order data, deployed via Kubernetes StatefulSet.         |

---

## ⚙️ Deployment Instructions

1. Clone all microservices to your local environment.
2. Build and push Docker images:
   ```bash
   docker build -t <your-dockerhub-username>/store-front ./store-front
   docker push <your-dockerhub-username>/store-front
   # Repeat for other services