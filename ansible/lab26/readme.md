# 🚀 Lab 26 - Initial Ansible Configuration and Ad-Hoc Execution

## 📖 Overview

This lab demonstrates the initial setup of Ansible by configuring a control node, creating SSH authentication, defining an inventory, and executing Ad-Hoc commands on a managed node.

---

## 🎯 Objectives

- Install Ansible.
- Generate SSH keys.
- Configure passwordless SSH authentication.
- Create an inventory file.
- Test connectivity using the ping module.
- Execute Ad-Hoc commands.
- Check disk space on the managed node.

---

## 📂 Project Structure

```text
lab26/
│
├── inventory
├── README.md

```

---

## ⚙️ Steps

### Install Ansible

```bash
sudo dnf install ansible-core -y
ansible --version
```

---

### Generate SSH Key

```bash
ssh-keygen -t rsa -b 4096
```


---

### Copy Public Key

```bash
ssh-copy-id student@192.168.1.20
ssh student@192.168.1.20
```

---

### Create Inventory

```ini
[servers]
managed ansible_host=192.168.1.20 ansible_user=student
```


---

### Test Connectivity

```bash
ansible all -i inventory -m ping
```

---

### Check Disk Space

```bash
ansible all -i inventory -a "df -h"
```

---

## 📚 Commands Used

```bash
ansible --version
ssh-keygen -t rsa -b 4096
ssh-copy-id student@192.168.1.20
ansible all -m ping
ansible all -a "df -h"
```

---

## 👨‍💻 Author

**Abdelrahman Tarek Ahmed**  
Cloud & DevOps Engineer