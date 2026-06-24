# 02 - Labels and Selectors

This example demonstrates how to use **Labels** and **Selectors** in Kubernetes. Labels are key-value pairs attached to objects such as Pods, and selectors are used to filter and identify resources based on those labels.

## What are Labels?

Labels are metadata attached to Kubernetes objects. They help organize and categorize resources.

Example:

```yaml
labels:
  app: nginx
  env: dev
```

In this example:

* `app: nginx` identifies the application.
* `env: dev` indicates that the Pod belongs to the development environment.

## Pod Manifest

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
  labels:
    app: nginx
    env: dev
spec:
  containers:
  - name: nginx
    image: nginx:latest
    ports:
    - containerPort: 80
```

## Deploy the Pod

Apply the manifest:

```bash
kubectl apply -f pod.yml
```

## Verify the Pod

```bash
kubectl get pods
```

Display labels associated with the Pod:

```bash
kubectl get pods --show-labels
```

## Using Label Selectors

Retrieve Pods with a specific label:

```bash
kubectl get pods -l app=nginx
```

Filter Pods by environment:

```bash
kubectl get pods -l env=dev
```

## Key Concepts

* **Labels** provide metadata to Kubernetes objects.
* **Selectors** use labels to identify and group resources.
* Services, ReplicaSets, and Deployments rely on label selectors to manage Pods.
* Labels enable flexible organization and efficient resource management.

## Learning Outcome

After completing this example, you will understand:

* How to assign labels to Pods.
* How to view labels using kubectl.
* How selectors filter resources based on labels.
* Why labels and selectors are fundamental to Kubernetes resource management.

