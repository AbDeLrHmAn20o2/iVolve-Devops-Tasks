# 🚀 Lab 23 - CI/CD Pipeline Implementation with Jenkins Agents and Shared Libraries

## 📖 Overview

This lab demonstrates how to implement a **Jenkins CI/CD Pipeline** using **Jenkins Agents** and **Shared Libraries**.

The pipeline uses a remote Jenkins Agent to execute the pipeline stages and uses Jenkins Shared Library to create reusable pipeline functions.

The pipeline contains the following stages:

1. BuildApp
2. BuildImage
3. DeployOnK8s

> **Note**
>
> Docker Hub Push and Kubernetes Deployment stages were intentionally skipped in this lab.  
> The main focus was configuring Jenkins Agents and implementing Shared Libraries.

---

# 🛠️ Technologies Used

- Jenkins
- Jenkins Pipeline
- Jenkins Shared Library
- Jenkins Agent (SSH)
- Git
- GitHub
- Docker
- Kubernetes

---

# 📂 Project Structure

```text
lab-23/
│── README.md
│── Jenkinsfile
│
├── Jenkins_App/
│   ├── Dockerfile
│   ├── deployment.yaml
│   ├── service.yaml
│   └── application files
│
├── jenkins-shared-lib/
│   └── vars/
│       ├── buildApp.groovy
│       ├── buildImage.groovy
│       └── deployK8s.groovy
│
└── screenshots/
    ├── 01-jenkins-agent.png
    ├── 02-shared-library-config.png
    ├── 03-pipeline-job.png
    ├── 04-build-now.png
    ├── 05-buildapp-stage.png
    ├── 06-buildimage-stage.png
    ├── 07-deploy-stage.png
    └── 08-pipeline-success.png
```

---

# Step 1 - Configure Jenkins Agent

A Jenkins SSH Agent was created to execute pipeline tasks remotely.

Agent configuration:

- Node Name: `docker-agent`
- Remote Directory: `/home/jenkins`
- Launch Method: SSH
- Label: `docker`

After configuration, the agent became online successfully.

### 📷 Screenshot

![Jenkins Agent](screenshots/Screenshot%202026-07-28%20195706.png)

---

# Step 2 - Configure Jenkins Shared Library

A shared library repository was created to store reusable pipeline functions.

Repository:

```
jenkins-shared-lib
```

Library configuration inside Jenkins:

```
Name:
jenkins-lib

Default Version:
main

Repository:
https://github.com/AbDeLrHmAn20o2/jenkins-shared-lib
```

### 📷 Screenshot

![Shared Library](screenshots/Screenshot%202026-07-28%20195332.png)

---

# Step 3 - Create Jenkins Pipeline Job

A new Jenkins Pipeline Job was created and configured to use the Jenkinsfile from GitHub.

The pipeline loads the shared library using:

```groovy
@Library('jenkins-lib') _
```


# Step 4 - Run the Pipeline

Click **Build Now** to start the pipeline execution.

Jenkins executes the pipeline stages using the configured Jenkins Agent.

### 📷 Screenshot

![Build Now](screenshots/Screenshot%202026-07-28%20195420.png)

---

# Step 5 - BuildApp Stage

The first shared library function executes the application build stage.

The function performs:

- Access project files
- Verify application structure
- Execute build commands


# Step 6 - BuildImage Stage

The pipeline calls the Docker image build function from the shared library.



# Step 7 - DeployOnK8s Stage

The pipeline calls the Kubernetes deployment function from the shared library.


# Step 8 - Pipeline Completed Successfully

After executing all shared library functions, Jenkins marks the pipeline as **SUCCESS**.

### 📷 Screenshot

![Pipeline Success](screenshots/Screenshot%202026-07-28%20195536.png)

---

# 📋 Pipeline Stages

- ✅ Jenkins Agent Configuration
- ✅ Shared Library Configuration
- ✅ BuildApp Stage
- ⏭️ BuildImage Stage (Skipped)
- ⏭️ DeployOnK8s Stage (Skipped)
- ✅ Pipeline Execution Successfully

---

# 📌 Expected Result

- Jenkins Agent connects successfully.
- Pipeline runs on the remote Jenkins Agent.
- Shared Library functions are loaded successfully.
- BuildApp stage executes successfully.
- Docker Build stage is skipped.
- Kubernetes Deployment stage is skipped.
- Jenkins Pipeline finishes successfully.

---

# 👨‍💻 Author

**Abdelrahman Tarek Ahmed**

Cloud & DevOps Engineer