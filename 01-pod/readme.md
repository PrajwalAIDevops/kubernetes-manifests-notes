# Kubernetes Pod Manifest

This YAML file is used to create a Pod in Kubernetes. A Pod is the smallest deployable unit in Kubernetes and can contain one or more containers.

## What this manifest does

* Creates a Pod.
* Pulls the specified Docker image.
* Starts the container inside the Pod.
* Assigns a name to the Pod.
* Exposes the application port inside the container.

## Components

### apiVersion

Specifies the Kubernetes API version used to create the resource.

### kind

Defines the type of resource being created, such as Pod, Deployment, or Service.

### metadata

Contains information about the resource, including its name and labels.

### spec

Describes the desired state of the Pod.

### containers

Defines the container image to run and its configuration.

### image

Specifies the Docker image that Kubernetes will pull and deploy.

### ports

Defines the container port used by the application.

## Deployment

Apply the manifest using:

```bash
kubectl apply -f pod.yml
```

Verify the Pod:

```bash
kubectl get pods
```

View logs:

```bash
kubectl logs <pod-name>
```

Delete the Pod:

```bash
kubectl delete -f pod.yml
```

This manifest provides a simple way to deploy and manage containerized applications in Kubernetes.

