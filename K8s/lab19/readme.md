# Lab 19: Node-Wide Pod Management with DaemonSet

## 📌 Objective

In this lab, we deploy **Prometheus Node Exporter** as a **DaemonSet** to ensure that one monitoring pod runs on **every node** in the Kubernetes cluster. The exporter exposes system metrics on **port 9100**, allowing Prometheus to collect node-level metrics.

---

# Prerequisites

- Kubernetes Cluster (Minikube with 2 Nodes)
- kubectl installed
- Running Kubernetes Cluster

Verify the cluster:

```bash
kubectl get nodes
```

---

# Project Structure

```text
lab19/
│── node-exporter.yaml
│── README.md
└── screenshots/
    ├── 01-cluster-nodes.png
    ├── 02-create-namespace.png
    ├── 03-deploy-daemonset.png
    ├── 04-daemonset-status.png
    ├── 05-pods-wide.png
    ├── 06-describe-daemonset.png
    ├── 07-node-ip.png
    └── 08-metrics.png
```

---

# Step 1 – Create Monitoring Namespace

Create a namespace named **monitoring**.

```bash
kubectl create namespace monitoring
```

Verify:

```bash
kubectl get ns
```

### Screenshot

![Create Namespace](screenshots/Screenshot%202026-07-22%20145021.png)

---

# Step 2 – Create the DaemonSet Manifest

Create a file named:

```text
node-exporter.yaml
```

Paste the following manifest:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: node-exporter
  namespace: monitoring
spec:
  selector:
    matchLabels:
      app: node-exporter
  template:
    metadata:
      labels:
        app: node-exporter
    spec:
      hostNetwork: true
      hostPID: true

      tolerations:
      - operator: Exists

      containers:
      - name: node-exporter
        image: prom/node-exporter:v1.8.2

        ports:
        - containerPort: 9100
          hostPort: 9100
          name: metrics

        args:
        - --path.rootfs=/host

        volumeMounts:
        - name: root
          mountPath: /host
          readOnly: true

      volumes:
      - name: root
        hostPath:
          path: /
```

---

# Step 3 – Deploy the DaemonSet

Deploy the manifest.

```bash
kubectl apply -f node-exporter.yaml
```

Expected Output

```text
daemonset.apps/node-exporter created
```

### Screenshot

![Deploy DaemonSet](screenshots/Screenshot%202026-07-22%20145057.png)

---

# Step 4 – Verify the DaemonSet

Check that Kubernetes created the DaemonSet.

```bash
kubectl get ds -n monitoring
```

Expected Output

```text
NAME            DESIRED   CURRENT   READY
node-exporter   2         2         2
```

### Screenshot

![DaemonSet Status](screenshots/Screenshot%202026-07-22%20145128.png)

---

# Step 5 – Verify Pods

List the running pods.

```bash
kubectl get pods -n monitoring -o wide
```

Example Output

```text
NAME                     READY   STATUS    NODE
node-exporter-abcde      1/1     Running   minikube
node-exporter-fghij      1/1     Running   minikube-m02
```

Notice that **one pod is running on every node**.

### Screenshot

![Pods Running](screenshots/Screenshot%202026-07-22%20145152.png)

---

# Step 6 – Describe the DaemonSet

Display detailed information.

```bash
kubectl describe ds node-exporter -n monitoring
```

Example

```text
Desired Number of Nodes Scheduled: 2
Current Number of Nodes Scheduled: 2
Number of Nodes Scheduled with Up-to-date Pods: 2
```

### Screenshot

![Describe DaemonSet](screenshots/Screenshot%202026-07-22%20145356.png)

---

# Step 7 – Get Node IP

Retrieve the node IP addresses.

```bash
kubectl get nodes -o wide
```

Example

```text
NAME           INTERNAL-IP
minikube       192.168.49.2
minikube-m02   192.168.49.3
```

### Screenshot

![Node IP](screenshots/Screenshot%202026-07-22%20145411.png)

---

# Step 8 – Verify Metrics

Access the metrics endpoint.

Using Node IP:

```bash
curl http://<NODE-IP>:9100/metrics
```

Or from inside the pod:

```bash
kubectl exec -it -n monitoring <node-exporter-pod> -- \
wget -qO- http://localhost:9100/metrics
```

Expected Output

```text
# HELP node_cpu_seconds_total
# TYPE node_cpu_seconds_total counter
node_cpu_seconds_total{cpu="0",mode="idle"} ...
```

### Screenshot

![Metrics Output](screenshots/Screenshot%202026-07-22%20145730.png)

---

# Validation Commands

## Check Nodes

```bash
kubectl get nodes
```

## Check DaemonSet

```bash
kubectl get ds -n monitoring
```

## Check Pods

```bash
kubectl get pods -n monitoring -o wide
```

## Describe DaemonSet

```bash
kubectl describe ds node-exporter -n monitoring
```

## Test Metrics

```bash
curl http://<NODE-IP>:9100/metrics
```

---

# Cleanup

Delete the DaemonSet

```bash
kubectl delete ds node-exporter -n monitoring
```

Delete the namespace

```bash
kubectl delete namespace monitoring
```

---

# Key Concepts

- **DaemonSet** ensures one Pod runs on every node.
- **hostNetwork** exposes port **9100** on the node.
- **hostPID** allows access to host process information.
- **hostPath** mounts the host filesystem inside the container.
- **tolerations** allow scheduling on tainted nodes.
- **Node Exporter** exposes CPU, Memory, Disk, Network, and System metrics for Prometheus.

---

# Lab Outcome

By completing this lab, you learned how to:

- Create a Kubernetes DaemonSet.
- Deploy Prometheus Node Exporter.
- Schedule one monitoring pod on every node.
- Configure tolerations for tainted nodes.
- Expose metrics on port **9100**.
- Validate monitoring across the Kubernetes cluster.