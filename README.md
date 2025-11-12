# 🚀 DevOps Capstone Project – CD & GitOps Repository

## 📘 Overview
This repository contains the **Continuous Deployment (CD)** and **Kubernetes GitOps configuration** for the DevOps Capstone Project.  
It automates application deployment and monitoring on an **AWS EKS cluster** using **ArgoCD, Helm, Vault, and Prometheus/Grafana**, ensuring secure, observable, and scalable delivery.

---

## ☸️ Kubernetes Architecture

### Namespaces

| Namespace | Purpose |
|-----------|---------|
| `vault` | HashiCorp Vault for secrets management |
| `capstoneapp` | Application deployments (frontend + MySQL) |
| `ingress` | Nginx Ingress Controller |
| `argocd` | ArgoCD GitOps operator |
| `monitoring` | Prometheus, Grafana, and AlertManager stack |

---

## 🧠 Deployment Machine (Machine 3)

### Installed Tools
- **kubectl, Helm**  
- **ArgoCD**  
- **Vault**  
- **Prometheus/Grafana** (via kube-prometheus-stack Helm chart)  

---

## 🔐 Secrets Management with Vault
- Vault deployed in **HA mode** using Helm.  
- Vault Agent Injectors are used to dynamically inject secrets (application credentials and database passwords) into pods.  
- Secrets are securely pulled into deployments without hardcoding sensitive data.

---

## 🧩 Application Deployment

### Components
- **Frontend:** Java Spring Boot application (`docker.io/danushvithiyarth/capstoneproject`)  
- **Database:** MySQL 8 container  
- **Ingress:** Nginx Ingress mapped to domain `https://danushvithiyarth.in`

### Manifests Included
- `frontendapp.yaml` → App deployment + service + Vault integration  
- `mysql.yaml` → MySQL deployment + Vault integration  
- `ingress.yaml` → Nginx Ingress configuration  
- `alert-rules.yaml` → Prometheus custom alerts  

---

## ⚙️ GitOps Workflow with ArgoCD
- ArgoCD deployed in the `argocd` namespace via Helm.  
- **Jenkins (from CI machine)** updates this repository with new Docker image tags.  
- ArgoCD automatically syncs updated manifests to the EKS cluster, ensuring the application is deployed with the latest changes.  

**Workflow Summary:**
1. Jenkins builds a new Docker image.  
2. Jenkins updates the image tag in Kubernetes manifest (`frontendapp.yaml`).  
3. ArgoCD detects the change and deploys the latest version to the cluster.  

---

## 📈 Monitoring & Alerting
- **Monitoring Stack:** Prometheus Operator (kube-prometheus-stack) and Grafana  
- **Alerts:** Configured via Prometheus AlertManager (example: pod not running, deployment unavailable)  
- Visualized via Grafana dashboards for node/pod health and resource utilization.  
- Alerts tested successfully for both firing and resolved states.  

---

## 🧩 Deployment Summary

| Component | Tool/Service | Namespace |
|-----------|-------------|-----------|
| Application | Java Spring Boot | capstoneapp |
| Database | MySQL 8 | capstoneapp |
| Ingress Controller | Nginx | ingress |
| Secret Management | Vault (HA Mode) | vault |
| GitOps | ArgoCD | argocd |
| Monitoring | Prometheus, Grafana, AlertManager | monitoring |

---

## 🧰 Tools & Technologies

| Category | Tools |
|----------|-------|
| Kubernetes | EKS, Helm |
| GitOps | ArgoCD |
| Secret Management | Vault |
| Monitoring | Prometheus, Grafana, AlertManager |
| Ingress | Nginx |
| Deployment | Helm, kubectl |
| Domain Management | Hostinger, Ingress LoadBalancer |
| CI/CD Integration | Jenkins (from CI repo) |

---

## 🌐 Repository Links

| Repository | Description |
|------------|-------------|
| [DevOps-Capstone-Project_CI](https://github.com/danushvithiyarth/DevOps-Capstone-Project_CI.git) | CI pipelines, Jenkins, Terraform |
| [DevOps-Capstone-Project_CD](https://github.com/danushvithiyarth/DevOps-Capstone-Project_CD.git) | Kubernetes manifests, GitOps setup, Vault, monitoring & alerts |

---

## 📝 Activity Log

This repository includes an **Activity Log** folder with screenshots and evidence of Kubernetes deployments, Vault secret injection, ArgoCD GitOps syncs, and monitoring dashboards:

- `Activity_Log_CD/` – Contains screenshots of application deployment, MySQL setup, ArgoCD sync, Prometheus/Grafana dashboards, and alert notifications.

---

## 🧾 Author

**👤 Danush Vithiyarth**  
💻 [GitHub: @danushvithiyarth](https://github.com/danushvithiyarth)

---

> 🧠 *This setup demonstrates a complete GitOps-based Continuous Deployment workflow — from automated application deployment on EKS to secure secret management with Vault and real-time monitoring via Prometheus and Grafana — representing a production-ready Kubernetes deployment pipeline.*
