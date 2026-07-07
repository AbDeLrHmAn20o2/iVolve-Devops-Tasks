# Lab 3: Run Java Spring Boot App in a Docker Container

## Objective

Run a Java Spring Boot application inside a Docker container using a Maven base image with Java 17.

---

# Prerequisites

- Docker
- Git

---

# Step 1: Clone the Repository

Clone the application source code.

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git

cd Docker-1
```

### Screenshot
![Step1](screenshots/clone.png)

---

# Step 2: Create Dockerfile

Create a file named **Dockerfile** in the project root.

### Screenshot
![Step2](screenshots/cat.png)

---

# Step 3: Build Docker Image

Build the Docker image.

```bash
docker build -t app1 .
```

### Screenshot
![Step3](screenshots/build.png)

---

# Step 4: Check Image Size

Display the created Docker image.

```bash
docker images
```

Example Output:

```
REPOSITORY   TAG      IMAGE ID      SIZE
app1         latest   xxxxxxxxx     1.2GB
```

### Screenshot
![Step4](screenshots/image.png)

---

# Step 5: Run Docker Container

Run the application container.

### Screenshot
![Step5](screenshots/create_container.png)

---

# Step 6: Test the Application

Open your browser and navigate to:

```
http://localhost:8080
```

or test using curl:

```bash
curl http://localhost:8080
```

### Screenshot
![Step6](screenshots/curl.png)

---

# Step 7: Stop & Remove the Container

```bash
docker stop container1
docker rm container1
```

### Screenshot
![Step7](screenshots/stop.png)

---

# Project Structure

```
Docker-1/
│
├── Dockerfile
├── pom.xml
├── src/
├── target/
└── README.md
```

---

# Docker Commands Summary

```bash
git clone https://github.com/Ibrahim-Adel15/Docker-1.git

cd Docker-1

docker build -t app1 .

docker images

docker run -d --name container1 -p 8080:8080 app1

docker ps

docker logs container1

docker stop container1

docker rm container1
```

---

# Technologies Used

- Java 17
- Spring Boot
- Maven
- Docker

---

# Author

**Abdelrhman Tarek Ahmed**

Faculty of Computers and Artificial Intelligence

Cloud & DevOps Engineer
