# 🚀 Lab 29 - Securing Sensitive Data with Ansible Vault

## 📖 Overview

This lab demonstrates how to secure sensitive information using **Ansible Vault** while automating the installation and configuration of a MySQL server. The playbook installs MySQL, creates a database and user, and stores sensitive credentials in an encrypted file.

---

## 🎯 Objectives

- Install MySQL using Ansible.
- Create the **iVolve** database.
- Create a MySQL user with full privileges on the database.
- Encrypt sensitive variables using **Ansible Vault**.
- Verify the database configuration.

---

## 📂 Project Structure

```text
lab29/
│
├── inventory
├── playbook.yml
├── vars/
│   └── db.yml
├── README.md

```

---

## ⚙️ Steps

### 1. Create Variables File

Store the database credentials in `vars/db.yml`.

![Vault Variables](screenshots/01-vault-file.png)

---

### 2. Encrypt the Variables File

```bash
ansible-vault encrypt vars/db.yml
```

![Vault Encrypt](screenshots/02-vault-encrypt.png)

---

### 3. Create the Playbook

The playbook performs the following tasks:

- Install MySQL.
- Start and enable the MySQL service.
- Create the **iVolve** database.
- Create a database user.
- Grant all privileges on the database.

![Playbook](screenshots/03-playbook.png)

---

### 4. Run the Playbook

```bash
ansible-playbook -i inventory playbook.yml --ask-vault-pass
```

> If `sudo` requires a password, use:

```bash
ansible-playbook -i inventory playbook.yml --ask-become-pass --ask-vault-pass
```

![Run Playbook](screenshots/04-run-playbook.png)

---

### 5. Verify MySQL Service

```bash
sudo systemctl status mysql
```

![MySQL Status](screenshots/05-mysql-status.png)

---

### 6. Verify the Database

```bash
sudo mysql
```

```sql
SHOW DATABASES;
```

![Databases](screenshots/06-show-databases.png)

---

### 7. Login with the Created User

```bash
mysql -u ivolve -p
```

```sql
SHOW DATABASES;
```

![Database User](screenshots/07-login-user.png)

---

## 📚 Commands Used

```bash
ansible-vault encrypt vars/db.yml

ansible-playbook -i inventory playbook.yml --ask-vault-pass

mysql -u ivolve -p

SHOW DATABASES;
```

---

## 👨‍💻 Author

**Abdelrahman Tarek Ahmed**  
Cloud & DevOps Engineer