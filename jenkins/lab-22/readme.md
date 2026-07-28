# 🚀 Lab 22 - Jenkins CI Pipeline for Java Spring Boot Application

## 📖 Overview

This lab demonstrates how to create a **Jenkins Declarative Pipeline** that automates the Continuous Integration (CI) workflow for a Java Spring Boot application.

The pipeline executes a sequence of automated stages to prepare the application for deployment.

> **Note**
>
> Docker Push and Kubernetes Deployment stages were intentionally skipped in this lab.

---

# 🛠️ Technologies Used

- Jenkins
- Git
- GitHub
- Declarative Pipeline
- Docker
- Java
- Maven

---

# 📂 Project Structure

```text
lab-22/
│── README.md
│── Jenkinsfile
│
├── Jenkins_App/
│   ├── Dockerfile
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── pom.xml
│   └── src/
│
└── screenshots/
    ├── 01-pipeline-job.png
    ├── 02-build-now.png
    ├── 03-clone-stage.png
    ├── 04-project-stage.png
    ├── 05-unit-test-stage.png
    ├── 06-build-stage.png
    ├── 07-build-image-stage.png
    ├── 08-delete-image-stage.png
    ├── 09-update-deployment-stage.png
    └── 10-pipeline-success.png
```

---

# Step 1 - Create Jenkins Pipeline

Create a new **Pipeline Job** inside Jenkins.

Configure the pipeline and add the Jenkinsfile.

### 📷 Screenshot

![Pipeline Job](screenshots/Screenshot%202026-07-28%20180950.png)

---

# Step 2 - Run the Pipeline

Click **Build Now** to start the pipeline execution.

Jenkins will execute each stage automatically.

### 📷 Screenshot

![Build Now](screenshots/Screenshot%202026-07-28%20181256.png)

---

# Step 3 - Clone Repository Stage

The pipeline clones the latest version of the project from GitHub using the configured credentials.

### 📷 Screenshot

![Clone Stage](screenshots/Screenshot%202026-07-28%20181512.png)

---

# Step 4 - Go To Project Stage

The pipeline navigates to the application directory before executing the remaining stages.

### 📷 Screenshot

![Project Directory Stage](screenshots/Screenshot%202026-07-28%20181531.png)

---

# Step 5 - Unit Test Stage

The pipeline executes the unit testing stage to validate the application before building.

### 📷 Screenshot

![Unit Test Stage](screenshots/Screenshot%202026-07-28%20181617.png)

---

# Step 6 - Build Application Stage

The application is compiled and packaged successfully.


---

# Step 7 - Build Docker Image Stage

The pipeline creates a Docker image for the application.

### 📷 Screenshot

![Build Docker Image](screenshots/Screenshot%202026-07-28%20181718.png)

---

# Step 8 - Delete Local Docker Image Stage

After the image is created, the local copy is removed from the Jenkins environment.

### 📷 Screenshot

![Delete Docker Image](screenshots/Screenshot%202026-07-28%20181740.png)

---

# Step 9 - Update Deployment Manifest Stage

The pipeline updates the image tag inside **deployment.yaml** with the latest version.

---

# Step 10 - Pipeline Completed Successfully

After all stages finish successfully, Jenkins marks the pipeline as **SUCCESS**.

### 📷 Screenshot

![Pipeline Success](screenshots/Screenshot%202026-07-28%20181829.png)
![Pipeline Success](screenshots/Screenshot%202026-07-28%20181315.png)

---

# 📋 Pipeline Stages

- ✅ Clone Repository
- ✅ Go To Project
- ✅ Unit Test
- ✅ Build Application
- ✅ Build Docker Image
- ✅ Delete Local Docker Image
- ✅ Update Deployment Manifest

---

# 📌 Expected Result

- Jenkins Pipeline executes successfully.
- Source code is cloned from GitHub.
- Application passes the CI workflow.
- Docker image is built successfully.
- Local Docker image is removed.
- Deployment manifest is updated with the latest image tag.
- Pipeline finishes successfully.

---

# 👨‍💻 Author

**Abdelrahman Tarek Ahmed**

Cloud & DevOps Engineer