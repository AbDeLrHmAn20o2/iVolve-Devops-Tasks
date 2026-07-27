# Lab 21: Role-Based Authorization in Jenkins

## Objective

Configure **Role-Based Access Control (RBAC)** in Jenkins by creating two users with different permission levels:

* **user1** → Administrator (Full Access)
* **user2** → Read-Only User

---

## Prerequisites

* Docker installed
* Jenkins Docker image
* Web browser

---

# Step 1: Create a Docker Volume

Create a persistent volume to store Jenkins data.

```bash
docker volume create jenkins_home
```

---

# Step 2: Run Jenkins Container

```bash
docker run -d \
  --name jenkins \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

Verify that Jenkins is running.

```bash
docker ps
```

---

# Step 3: Retrieve the Initial Admin Password

```bash
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

Copy the generated password.

---

# Step 4: Access Jenkins

Open your browser and navigate to:

```
http://localhost:8080
```

* Paste the initial admin password.
* Click **Continue**.
* Select **Install suggested plugins**.
* Wait for the installation to finish.
* Create the first administrator account.

---

# Step 5: Install Role-Based Authorization Plugin

Navigate to:

**Manage Jenkins → Plugins → Available Plugins**

Search for:

```
Role-based Authorization Strategy
```

Install the plugin.

Restart Jenkins if prompted.

📷 **Screenshot:** Plugin Installation

---

# Step 6: Enable Role-Based Authorization

Navigate to:

**Manage Jenkins → Security**

Under **Authorization**, select:

```
Role-Based Strategy
```

Click **Save**.

![](screenshots/Screenshot%202026-07-27%20202314.png)

---

# Step 7: Create Users

Navigate to:

**Manage Jenkins → Security → Users**

Create the following users.

### User 1

| Field     | Value     |
| --------- | --------- |
| Username  | user1     |
| Password  | user1@123 |
| Full Name | User One  |

---

### User 2

| Field     | Value     |
| --------- | --------- |
| Username  | user2     |
| Password  | user2@123 |
| Full Name | User Two  |

![](screenshots/Screenshot%202026-07-27%20202242.png)

---

# Step 8: Create Roles

Navigate to:

**Manage Jenkins → Manage and Assign Roles → Manage Roles**

Create the following roles.

---

## Admin Role

Grant the following permissions:

* Overall → Administer
* Overall → Read
* Job → All
* View → All

---

## ReadOnly Role

Grant the following permissions:

* Overall → Read
* Job → Read
* View → Read

![](screenshots/Screenshot%202026-07-27%20202431.png)

---

# Step 9: Assign Roles

Navigate to:

**Manage Jenkins → Manage and Assign Roles → Assign Roles**

Assign the roles as follows.

| User  | Role     |
| ----- | -------- |
| user1 | admin    |
| user2 | readonly |

Save the configuration.

![](screenshots/Screenshot%202026-07-27%20202149.png)

---

# Step 10: Verify Access

## Login as user1

Expected capabilities:

* Create Jobs
* Delete Jobs
* Configure Jenkins
* Install Plugins
* Manage Users

![](screenshots/Screenshot%202026-07-27%20203050.png)

---

## Login as user2

Expected capabilities:

* View Jobs
* View Build History
* View Console Output

Restrictions:

* Cannot create jobs
* Cannot delete jobs
* Cannot configure Jenkins
* Cannot install plugins
* Cannot manage users

![](screenshots/Screenshot%202026-07-27%20203124.png)

---

# Verification

| Username | Role      | Access      |
| -------- | --------- | ----------- |
| user1    | Admin     | Full Access |
| user2    | Read Only | View Only   |

---

# Result

Successfully configured **Role-Based Authorization (RBAC)** in Jenkins using the **Role-Based Authorization Strategy** plugin.

Two users were created with different permission levels:

* **user1** → Full Administrator
* **user2** → Read-Only User

This setup improves security by ensuring users only receive the permissions required for their responsibilities, following the **Principle of Least Privilege (PoLP)**.
