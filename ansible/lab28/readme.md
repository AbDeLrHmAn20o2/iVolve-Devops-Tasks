# 🚀 Lab 28 - Structured Configuration Management with Ansible Roles

## 📖 Overview

This lab demonstrates how to organize Ansible automation using **Roles**. Separate roles were created to automate the installation and configuration of Docker, Kubernetes CLI (`kubectl`), and Jenkins, then executed through a single Ansible playbook.

---

## 🎯 Objectives

- Create Ansible Roles.
- Configure Docker using a Role.
- Configure Kubernetes CLI (`kubectl`) using a Role.
- Configure Jenkins using a Role.
- Execute all roles from a single playbook.
- Verify the installed tools.

---

## 📂 Project Structure

```text
lab28/
│
├── inventory
├── playbook.yml
├── README.md
├── docker/
├── kubectl/
├── jenkins/
```

---

## ⚙️ Steps

### Create Ansible Roles

```bash
ansible-galaxy init docker
ansible-galaxy init kubectl
ansible-galaxy init jenkins
```
---

### Configure Docker Role

Create the Docker role to install and start Docker.

---

### Configure kubectl Role

Create the Kubernetes CLI role.
---

### Configure Jenkins Role

Create the Jenkins role.

---

### Create the Playbook

Run all roles from a single playbook.

```bash
ansible-playbook -i inventory playbook.yml
```

---

### Execute the Playbook

```bash
ansible-playbook -i inventory playbook.yml
```


---

### Verify Docker

```bash
docker --version
```

---

### Verify kubectl

```bash
kubectl version --client
```

---

### Verify Jenkins

```bash
systemctl status jenkins
```

or

```bash
jenkins --version
```

---

## 📚 Commands Used

```bash
ansible-galaxy init docker
ansible-galaxy init kubectl
ansible-galaxy init jenkins

ansible-playbook -i inventory playbook.yml

docker --version

kubectl version --client

systemctl status jenkins
```

---

## 👨‍💻 Author

**Abdelrahman Tarek Ahmed**  
Cloud & DevOps Engineer