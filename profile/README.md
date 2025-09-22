# blend:it

This is a project for [Therap Javafest 2025](https://www.therapjavafest.com/) by Team_ChocolateBoys.

Blend:it is a cloud-native pipeline for generating and processing `.blend` assets, integrating backend services, 3D rendering automation, and message-driven workflows. The project is designed to run on **Google Kubernetes Engine (GKE Autopilot)** with scalability and reliability in mind.

[Click here](https://www.youtube.com/watch?v=ZNub_PMqeaw) to watch the Full Project Demonstration

---

## 🚀 Technologies Used

### ☁️ Cloud & Infrastructure
- **Google Kubernetes Engine (GKE Autopilot)** – managed Kubernetes cluster
- **Cluster Autoscaler** – automatic scaling of pods/nodes
- **Load Balancer** – single entrypoint for services
- **Secrets & ConfigMaps** – for secure credentials and configuration

### 🖥 Backend
- **Java 24** with **Spring Boot**
  - REST APIs
  - Security (CORS, CSRF config, JWT planned)
- **Maven** – build and dependency management

### 📩 Messaging & Queueing
- **RabbitMQ** – message broker for asynchronous job handling
- Kubernetes **Service** & **Secret** integration for RabbitMQ access

### 🎨 3D Rendering & Asset Pipeline
- **Blender** – `.blend` file generation and processing
- **Python** – for Blender scripting and asset automation
- **Google Cloud Storage (GCS)** – storing `.blend` files and outputs

### 🛠 DevOps & Tooling
- **kubectl** – Kubernetes CLI for deployments and troubleshooting
- **YAML manifests** – Deployment, Service, and Autopilot resource configs
- **Spring Data** – database integration (future scope)

---

## 📂 Project Structure (High-Level)

- `blender-pipeline-service/` → Handles `.blend` generation/upload  
- `ai-service/` → AI-related processing (integrated with Blender pipeline)  
- `rabbitmq/` → Messaging queue setup and configs  
- `k8s-manifests/` → Kubernetes deployment & service YAML files  

---



# Backend Design

</br>

<img width="2894" height="1506" alt="image" src="https://github.com/user-attachments/assets/7ee95502-4c83-4ef1-ba16-ff90c39044b3" />

# Worker App Design

The **Blend:it Worker App** is a desktop application built with **Electron** that connects to the Blend:it pipeline. It acts as a worker node, pulling jobs from the queue, executing them (e.g., Blender rendering, asset processing), and sending results back to the cloud.

---

## ⚡ Features

- **Cross-platform desktop app** powered by Electron  
- Executes Blender/Python scripts locally for rendering tasks  
- Uploads output files (images, `.blend`, assets) to **Google Cloud Storage**  
- Provides a minimal UI for worker status and logs  

---

## 🛠 Technologies Used

- **Electron** – cross-platform desktop framework  
- **Node.js** – runtime for app logic  
- **Blender (CLI)** – for rendering and script execution  
- **Python** – Blender scripting integration  
- **REST API** – communication with Blend:it backend  

---

## 📂 Project Structure

- `main.js` → Electron main process (window + job handling)  
- `renderer/` → UI components (status, logs, controls)  
- `worker/` → Job processor that integrates with Blender CLI and scripts  
- `config/` → RabbitMQ + API configs  

---

## ▶️ Running the App

### Prerequisites
- [Node.js](https://nodejs.org/) (LTS recommended)  
- [Blender](https://www.blender.org/download/) installed and accessible via CLI  

### Steps
```bash
# Install dependencies
npm install

# Run in development mode
npm start

# Build distributable app
npm run build
```

</br>

<img width="1739" height="2002" alt="image" src="https://github.com/user-attachments/assets/69c4c732-964f-4b72-a11a-eef9ca909059" />

# Workflow and Frontend

</br>

<img width="2045" height="2400" alt="image" src="https://github.com/user-attachments/assets/5287b2a8-3507-42f4-b5b6-bb668c734a62" />


# P. S.

The backend is not fully uploaded to GKE for resource limitations. Only authentication and worker handler is up and running. To test it 
you can go to these urls and make api request for login, signup and email verification. Also worker can pull jobs from the server. But
users currently cannot upload their files as the microservice is not yet running in Google kubernetes engine. It runs fine on a local network

# We have added javafest@therapservices.net as admin in our kubenetes cluster

http://34.171.206.206:80/auth/signup
`POST`
```json
{
    "userId": "anything-unique",
    "email": "your-email",
    "password": "HelloWorld",
    "fullName": "You Name"
}
```


http://34.171.206.206:80/auth/verify `POST`
```json
{
    "email": "your-email"
}
```


http://34.171.206.206:80/auth/verify/confirm `POST`
```json
{
    "verificationCode": 123456,
    "email": "your-email"
}
```

http://34.171.206.206:80/auth/login `POST`
```json
{
    "email": "your-email",
    "password": "HelloWorld"
}
```
http://34.171.206.206:80/users/me `GET`
with Authorization Header Bearer Token \

http://34.171.206.206:80/users/ `GET`
with Authorization Header Bearer Token \

http://34.171.206.206:80/public/ `GET` to see total users in our service


> **Members:** \
> Pritom Das \
> Zubayer Hussain Uday
