# 🚀 Lab 30 - Automated Host Discovery with Ansible Dynamic Inventory

## 📖 Overview

This lab demonstrates how to use **Ansible Dynamic Inventory** to automatically discover AWS EC2 instances based on tags and manage them without maintaining a static inventory file. The discovered EC2 instances are then configured using an Ansible MySQL role.

---

## 🎯 Objectives

- Create an AWS EC2 instance.
- Tag the EC2 instance with `service=db`.
- Configure Ansible Dynamic Inventory.
- Discover running EC2 instances automatically.
- Execute the MySQL role.
- Verify the MySQL installation.

---

## 📂 Project Structure

```text
lab30/
│
├── ansible.cfg
├── aws_ec2.yml
├── playbook.yml
├── README.md
├── roles/
│   └── mysql/
│       └── tasks/
│           └── main.yml

```

---

## ⚙️ Steps

### 1. Install the Required Collection

```bash
ansible-galaxy collection install amazon.aws
```

---

### 2. Configure AWS Credentials

```bash
aws configure
```

Provide:

- AWS Access Key ID
- AWS Secret Access Key
- Default Region
- Output Format

---

### 3. Create an EC2 Instance

Launch an EC2 instance and ensure it is in the **Running** state.

---

### 4. Add the Required Tag

Assign the following tag to the EC2 instance:

| Key | Value |
|------|-------|
| service | db |

---

### 5. Configure Dynamic Inventory

Create the `aws_ec2.yml` inventory configuration.

---

### 6. List the Target Hosts

```bash
ansible-inventory --graph
```

or

```bash
ansible-inventory --list
```

---

### 7. Run the Playbook

```bash
ansible-playbook playbook.yml
```

---

### 8. Verify MySQL Installation

```bash
ansible tag_db -a "mysql --version"
```

or

```bash
ansible tag_db -a "systemctl status mysql"
```

---

## 📚 Commands Used

```bash
ansible-galaxy collection install amazon.aws

pip install boto3 botocore

aws configure

ansible-inventory --graph

ansible-inventory --list

ansible-playbook playbook.yml
```

---

## 👨‍💻 Author

**Abdelrahman Tarek Ahmed**  
Cloud & DevOps Engineer