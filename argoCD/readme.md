# 🚀 Lab 25 - GitOps Workflow with Jenkins and ArgoCD

## 📖 Overview

This lab demonstrates a complete **GitOps workflow** using **Jenkins**, **GitHub**, **ArgoCD**, and **Kubernetes (Minikube)**.

The Jenkins pipeline automates the deployment workflow by updating Kubernetes manifests stored in a GitHub repository. ArgoCD continuously monitors the repository and automatically synchronizes changes with the Kubernetes cluster.

> **Note**
>
> Docker Hub push was intentionally skipped in this lab. The purpose of this lab is to demonstrate the GitOps workflow and automatic synchronization using ArgoCD.

---

# 🎯 Objectives

- Install and configure ArgoCD
- Create a Jenkins Pipeline
- Build Docker Image
- Update Kubernetes Deployment Manifest
- Push changes to GitHub
- Automatically synchronize changes using ArgoCD

---

# 🛠 Technologies Used

- Jenkins
- GitHub
- Docker
- Kubernetes (Minikube)
- ArgoCD
- Git

---

# 📂 Repository Structure

```text
argoCd-lab/
│
├── Jenkinsfile
├── deployment.yaml
├── service.yaml
├── README.md
└── screenshots/
    ├── 01-jenkins-pipeline.png
    ├── 02-stage-view.png
    ├── 03-github-commit.png
    ├── 04-deployment-yaml.png
    ├── 05-argocd-application.png
    ├── 06-argocd-sync.png
    ├── 07-pods.png
    ├── 08-deployments.png
    └── 09-services.png
```

---

# ⚙️ Install ArgoCD

Create the ArgoCD namespace.

```bash
kubectl create namespace argocd
```

Install ArgoCD.

```bash
kubectl apply -n argocd \
-f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Verify installation.

```bash
kubectl get pods -n argocd
```

---

# 🔑 Access ArgoCD

Forward the ArgoCD service.

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open

```text
https://localhost:8080
```

Retrieve the admin password.

```bash
kubectl -n argocd get secret argocd-initial-admin-secret \
-o jsonpath="{.data.password}" | base64 -d
```

Username

```text
admin
```

---

# ⚙️ Configure ArgoCD Application

Create a new application with the following configuration.

| Field | Value |
|-------|-------|
| Application Name | gitops-app |
| Project | default |
| Sync Policy | Automatic |
| Repository URL | GitHub Repository |
| Revision | main |
| Path | . |
| Cluster URL | https://kubernetes.default.svc |
| Namespace | default |

---

# ⚙️ Jenkins Pipeline

The Jenkins pipeline performs the following stages:

1. Checkout Repository
2. Build Application *(Skipped if Maven project does not exist)*
3. Build Docker Image *(Skipped if Dockerfile does not exist)*
4. Load Docker Image into Minikube *(Optional)*
5. Delete Local Docker Image
6. Update `deployment.yaml`
7. Commit Changes
8. Push Changes to GitHub

---

# 🔄 GitOps Workflow

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ├── Checkout Source Code
    ├── Build Application
    ├── Build Docker Image
    ├── Update deployment.yaml
    ├── Commit Changes
    └── Push Changes
            │
            ▼
GitHub Repository
            │
            ▼
ArgoCD
            │
            ▼
Kubernetes Cluster
```

---

# ✅ Verify Deployment

Check Pods

```bash
kubectl get pods
```

Check Deployments

```bash
kubectl get deployments
```

Check Services

```bash
kubectl get svc
```

---

# 📸 Screenshots

## Jenkins Pipeline Success

![Jenkins Pipeline](screenshots/Screenshot%202026-08-01%20020941.png)
![Jenkins Pipeline](screenshots/Screenshot%202026-08-01%20021349.png)


---

## Updated Deployment Manifest

![Deployment YAML](screenshots/Screenshot%202026-08-01%20021055.png)

---

## ArgoCD Application

![ArgoCD Application](screenshots/Screenshot%202026-08-01%20021407.png)

---

## Kubernetes Pods

![Pods](screenshots/Screenshot%202026-08-01%20021222.png)

---

---

# ✅ Result

Successfully implemented a GitOps workflow using **Jenkins**, **GitHub**, **ArgoCD**, and **Kubernetes**.

The Jenkins pipeline automatically updates the Kubernetes deployment manifest stored in GitHub. ArgoCD continuously monitors the repository and synchronizes any detected changes with the Kubernetes cluster, providing an automated and declarative deployment workflow.

> **Docker Hub push was intentionally skipped in this lab to focus on the GitOps workflow and ArgoCD synchronization process.**