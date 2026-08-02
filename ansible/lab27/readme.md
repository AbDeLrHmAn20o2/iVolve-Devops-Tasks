# 🚀 Lab 27 - Automated Web Server Configuration Using Ansible Playbooks

## 📖 Overview

This lab demonstrates how to automate the installation and configuration of an Nginx web server using an Ansible Playbook. The playbook installs Nginx, starts and enables the service, deploys a custom web page, and verifies that the web server is running correctly.

---

## 🎯 Objectives

- Install Nginx using Ansible.
- Start and enable the Nginx service.
- Deploy a custom HTML page.
- Verify the web server configuration.

---

## 📂 Project Structure

```text
lab27/
│
├── inventory
├── playbook.yml
├── index.html
├── README.md
└── screenshots/
    ├── 01-playbook-success.png
    ├── 03-curl-test.png
```

---

## ⚙️ Steps

### 1. Create the Inventory

```ini
[web]
localhost ansible_connection=local
```

---

### 2. Create the Playbook

Create a playbook to:

- Install Nginx.
- Start and enable the Nginx service.
- Copy the custom HTML page.

---

### 3. Run the Playbook

```bash
ansible-playbook -i inventory playbook.yml
```

![Run Playbook](screenshots/Screenshot%202026-08-02%20191632.png)

---

### 4. Verify Nginx Status

```bash
sudo systemctl status nginx
```

> If your WSL environment does not use `systemd`, use:

```bash
service nginx status
```
---

### 5. Test the Web Page

```bash
curl http://localhost
```

![Curl Test](screenshots/Screenshot%202026-08-02%20191657.png)

---

### 6. Verify in Browser

Open:

```text
http://localhost
```


---

## 📚 Commands Used

```bash
ansible-playbook -i inventory playbook.yml

sudo systemctl status nginx

service nginx status

curl http://localhost
```

---

## 👨‍💻 Author

**Abdelrahman Tarek Ahmed**  
Cloud & DevOps Engineer