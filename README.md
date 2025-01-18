# Deploy a MERN Application using AKS

This repository contains the documentation and steps to deploy a MERN (MongoDB, Express, React, Node.js) application using Azure Kubernetes Service (AKS). The deployment process includes setting up the infrastructure, deploying the application, and verifying the functionality. All the steps are accompanied by screenshots for clarity.

## Table of Contents

1. [Introduction](#introduction)  
2. [Features](#features)  
3. [Prerequisites](#prerequisites)  
4. [Setup and Deployment](#setup-and-deployment)  
   - [Step 1: Clone the Application](#step-1-clone-the-application)  
   - [Step 2: Create AKS Cluster](#step-2-create-aks-cluster)  
   - [Step 3: Configure kubectl](#step-3-configure-kubectl)  
   - [Step 4: Deploy Application on AKS](#step-4-deploy-application-on-aks)  
   - [Step 5: Expose Application](#step-5-expose-application)  
   - [Step 6: Verify Deployment](#step-6-verify-deployment)  
5. [Screenshots](#screenshots)  
6. [Conclusion](#conclusion)

---

## Introduction

This project involves deploying a MERN application to Azure Kubernetes Service (AKS) to achieve scalability and efficient resource management. The application demonstrates microservices architecture and is hosted on a GitHub repository for ease of access.  

**Link to the application:** [SampleMERNwithMicroservices](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices)

---

## Features

- Deployment of a full-stack MERN application  
- Use of Azure Kubernetes Service (AKS) for container orchestration  
- Microservices-based architecture  
- Scalability and high availability  

---

## Prerequisites

Ensure you have the following before starting:

- Azure Subscription  
- Azure CLI installed  
- kubectl installed  
- Docker installed  
- Git installed  
- Access to the [GitHub repository](https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices)  

---

## Setup and Deployment

### Step 1: Clone the Application

1. Clone the repository to your local machine:  
   ```bash
   git clone https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices.git
   ```
2. Navigate to the project directory:
   ```bash
   cd SampleMERNwithMicroservices
   ```

### Step 2: Create AKS Cluster

1. Log in to your Azure account:
   ```bash
   az login
   ```
2. Create a resource group:
   ```bash
   az group create --name MERNResourceGroup --location eastus
   ```
3. Create an AKS cluster:
   ```bash
   az aks create --resource-group MERNResourceGroup --name MERNCluster --node-count 2 --enable-addons monitoring --generate-ssh-keys
   ```

### Step 3: Configure kubectl

1. Connect to the AKS cluster:
   ```bash
   az aks get-credentials --resource-group MERNResourceGroup --name MERNCluster
   ```
2. Verify the connection:
   ```bash
   kubectl get nodes
   ```
### Step 4: Deploy Application on AKS

1. Build Docker images for the application components:
   ```bash
   docker build -t <docker-hub-username>/mern-frontend ./frontend
   docker build -t <docker-hub-username>/mern-backend ./backend
   ```
2. Push the images to Docker Hub:
   ```bash
   docker push <docker-hub-username>/mern-frontend
   docker push <docker-hub-username>/mern-backend
   ```
3. Create Kubernetes deployment and service files in YAML format for each component.
4. Apply the YAML files:
   ```bash
   kubectl apply -f deployment-frontend.yaml
   kubectl apply -f deployment-backend.yaml
   ```
### Step 5: Expose Application

1. Expose the frontend service as a LoadBalancer:
   ```bash
   kubectl expose deployment mern-frontend --type=LoadBalancer --name=frontend-service
   ```
2. Get the external IP address of the service:
   ```bash
   kubectl get service frontend-service
   ```


