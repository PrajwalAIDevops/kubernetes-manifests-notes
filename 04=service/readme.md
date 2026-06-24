# Kubernetes NodePort Service Example

This repository contains a simple Kubernetes Service manifest that exposes an application running in a Pod using a **NodePort Service**.

## Service Manifest

```yaml
apiVersion: v1
kind: Service
metadata:
  name: html-svc
  labels:
    app: html-svc

spec:
  selector:
    app: html-web

  ports:
    - port: 80
      targetPort: 80

  type: NodePort
```

---

# What This Configuration Does

This Service exposes Pods with the label:

```yaml
app: html-web
```

and makes them accessible through a Kubernetes NodePort.

---

# Configuration Breakdown

## apiVersion

```yaml
apiVersion: v1
```

Specifies the Kubernetes API version used to create the Service resource.

---

## kind

```yaml
kind: Service
```

Defines the Kubernetes resource type.

In this case:

* `Service` provides network access to Pods.
* It creates a stable endpoint for applications.

---

## metadata

```yaml
metadata:
  name: html-svc
  labels:
    app: html-svc
```

### name

```yaml
name: html-svc
```

The name assigned to the Service.

You can view it using:

```bash
kubectl get svc
```

### labels

```yaml
labels:
  app: html-svc
```

Labels are used to organize and identify Kubernetes resources.

---

## spec

The `spec` section defines how the Service behaves.

### selector

```yaml
selector:
  app: html-web
```

The Service forwards traffic to Pods that have the label:

```yaml
app: html-web
```

Example Pod label:

```yaml
metadata:
  labels:
    app: html-web
```

---

## ports

```yaml
ports:
  - port: 80
    targetPort: 80
```

### port

```yaml
port: 80
```

The port exposed by the Service inside the cluster.

### targetPort

```yaml
targetPort: 80
```

The container port on the selected Pods that receives the traffic.

Traffic Flow:

```text
Client
   |
   v
Service Port (80)
   |
   v
Pod Port (80)
```

---

## type

```yaml
type: NodePort
```

Exposes the Service externally using a port on each Kubernetes Node.

Kubernetes automatically assigns a port from:

```text
30000 - 32767
```

Example:

```text
Node IP: 192.168.1.10
NodePort: 31234
```

Access the application:

```text
http://192.168.1.10:31234
```

---

# Deployment Steps

## 1. Create the Service

```bash
kubectl apply -f service.yaml
```

Expected Output:

```bash
service/html-svc created
```

---

## 2. Verify the Service

```bash
kubectl get svc
```

Example Output:

```bash
NAME       TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
html-svc   NodePort   10.96.120.101   <none>        80:31234/TCP   1m
```

---

## 3. Check Service Details

```bash
kubectl describe svc html-svc
```

---

## 4. Verify Endpoints

```bash
kubectl get endpoints html-svc
```

Example:

```bash
NAME       ENDPOINTS         AGE
html-svc   10.244.0.5:80     1m
```

---

## 5. Access the Application

Get node information:

```bash
kubectl get nodes -o wide
```

Open in browser:

```text
http://<NODE-IP>:<NODEPORT>
```

Example:

```text
http://192.168.1.10:31234
```

---

# Useful Commands

### List Services

```bash
kubectl get svc
```

### Describe Service

```bash
kubectl describe svc html-svc
```

### View Pods

```bash
kubectl get pods
```

### View Pod Labels

```bash
kubectl get pods --show-labels
```

### Check Endpoints

```bash
kubectl get endpoints html-svc
```

### Delete Service

```bash
kubectl delete svc html-svc
```

---

# Architecture

```text
                +----------------+
                |     Client     |
                +--------+-------+
                         |
                         v
                +----------------+
                |  NodePort SVC  |
                |    html-svc    |
                +--------+-------+
                         |
                         v
                +----------------+
                | Pod (html-web) |
                |    Port 80     |
                +----------------+
```

---

# Prerequisites

* Kubernetes Cluster
* kubectl installed and configured
* Running Pods with label:

```yaml
app: html-web
```

Example verification:

```bash
kubectl get pods --show-labels
```

---

