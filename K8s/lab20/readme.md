# Lab 20: Securing Kubernetes with RBAC and Service Accounts

## 📌 Objective

In this lab, we configure **Role-Based Access Control (RBAC)** in Kubernetes by creating a **Service Account**, generating an authentication token, defining a **Role** with read-only access to Pods, and binding the Role to the Service Account. Finally, we validate that the Service Account can only list and get Pods within the namespace.

---

# Prerequisites

- Kubernetes Cluster (Minikube with 2 Nodes)
- kubectl installed
- Running Kubernetes Cluster

Verify the cluster:

```bash
kubectl get nodes
```

# Project Structure

```text
lab20/
│── pod-reader-role.yaml
│── pod-reader-binding.yaml
│── README.md
└── screenshots/
    ├── 01-cluster-nodes.png
    ├── 02-create-namespace.png
    ├── 03-create-serviceaccount.png
    ├── 04-create-token.png
    ├── 05-create-role.png
    ├── 06-create-rolebinding.png
    ├── 07-create-pods.png
    ├── 08-list-pods.png
    ├── 09-can-i-list.png
    ├── 10-can-i-delete.png
```

---

# Step 1 – Create Namespace

Create the **ivolve** namespace.

```bash
kubectl create namespace ivolve
```

Verify:

```bash
kubectl get ns
```

### Screenshot

![Create Namespace](screenshots/Screenshot%202026-07-22%20151737.png)

---

# Step 2 – Create Service Account

Create a Service Account named **jenkins-sa**.

```bash
kubectl create serviceaccount jenkins-sa -n ivolve
```

Verify:

```bash
kubectl get sa -n ivolve
```

Expected Output

```text
NAME         SECRETS   AGE
default      0         1m
jenkins-sa   0         5s
```

### Screenshot

![Create Service Account](screenshots/Screenshot%202026-07-22%20151813.png)

---

# Step 3 – Generate a Service Account Token

Generate a token for the Service Account.

```bash
kubectl create token jenkins-sa -n ivolve
```

Example Output

```text
eyJhbGciOiJSUzI1NiIsImtpZCI6...
```

> **Note:** The generated token can be used by applications such as Jenkins to authenticate with the Kubernetes API.

### Screenshot

![Generate Token](screenshots/Screenshot%202026-07-22%20151853.png)

---

# Step 4 – Create the Role

Create a file named **pod-reader-role.yaml**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: pod-reader
  namespace: ivolve
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs:
    - get
    - list
```

Deploy the Role.

```bash
kubectl apply -f pod-reader-role.yaml
```

Verify:

```bash
kubectl get role -n ivolve
```

### Screenshot

![Create Role](screenshots/Screenshot%202026-07-22%20151934.png)

---

# Step 5 – Create the RoleBinding

Create a file named **pod-reader-binding.yaml**

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-binding
  namespace: ivolve

subjects:
- kind: ServiceAccount
  name: jenkins-sa
  namespace: ivolve

roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: pod-reader
```

Deploy the RoleBinding.

```bash
kubectl apply -f pod-reader-binding.yaml
```

Verify:

```bash
kubectl get rolebinding -n ivolve
```

### Screenshot

![Create RoleBinding](screenshots/Screenshot%202026-07-22%20152041.png)

---

# Step 6 – Create a Test Deployment

Deploy an Nginx application for testing.

```bash
kubectl create deployment nginx --image=nginx -n ivolve
```

Verify:

```bash
kubectl get pods -n ivolve
```

### Screenshot

![Pods](screenshots/Screenshot%202026-07-22%20152114.png)

---

# Step 7 – Validate Permissions

Verify that the Service Account can **list Pods**.

```bash
kubectl auth can-i list pods \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

Expected Output

```text
yes
```

Verify that it can **get Pods**.

```bash
kubectl auth can-i get pods \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

Expected Output

```text
yes
```

### Screenshot

![Can List Pods](screenshots/Screenshot%202026-07-22%20152146.png)
![Can get Pods](screenshots/Screenshot%202026-07-22%20152156.png)

---

# Step 8 – Verify Restricted Access

Attempt to delete Pods.

```bash
kubectl auth can-i delete pods \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

Expected Output

```text
no
```

Attempt to create Pods.

```bash
kubectl auth can-i create pods \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

Expected Output

```text
no
```

Attempt to list Deployments.

```bash
kubectl auth can-i list deployments \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

Expected Output

```text
no
```

### Screenshot

![Cannot Delete Pods](screenshots/Screenshot%202026-07-22%20152225.png)

### Screenshot

![Restricted Access](screenshots/Screenshot%202026-07-22%20152212.png)

![deploy Access](screenshots/Screenshot%202026-07-22%20152237.png)
---

# Validation Commands

Check Service Accounts

```bash
kubectl get sa -n ivolve
```

Check Roles

```bash
kubectl get role -n ivolve
```

Check RoleBindings

```bash
kubectl get rolebinding -n ivolve
```

Check Pods

```bash
kubectl get pods -n ivolve
```

Check Permissions

```bash
kubectl auth can-i list pods \
--as=system:serviceaccount:ivolve:jenkins-sa \
-n ivolve
```

---

# Cleanup

Delete the Deployment

```bash
kubectl delete deployment nginx -n ivolve
```

Delete the RoleBinding

```bash
kubectl delete rolebinding pod-reader-binding -n ivolve
```

Delete the Role

```bash
kubectl delete role pod-reader -n ivolve
```

Delete the Service Account

```bash
kubectl delete serviceaccount jenkins-sa -n ivolve
```

Delete the Namespace

```bash
kubectl delete namespace ivolve
```

---

# Key Concepts

- **RBAC (Role-Based Access Control)** controls access to Kubernetes resources.
- **Service Account** provides an identity for applications running in Kubernetes.
- **Role** defines permissions within a namespace.
- **RoleBinding** assigns a Role to a user, group, or Service Account.
- **kubectl auth can-i** is used to verify RBAC permissions.
- Authentication is performed using a **Service Account Token**.

---

# Lab Outcome

By completing this lab, you learned how to:

- Create a Kubernetes Service Account.
- Generate a Service Account token.
- Create a Role with read-only access to Pods.
- Bind the Role to a Service Account using a RoleBinding.
- Validate RBAC permissions using `kubectl auth can-i`.
- Restrict Kubernetes access following the principle of least privilege.