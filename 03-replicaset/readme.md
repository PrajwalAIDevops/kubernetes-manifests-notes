# Scaling Commands in Kubernetes

### Scale Up

```bash
kubectl scale deployment html-deploy --replicas=5
```

**Explanation:**
Increases the number of Pod replicas managed by the Deployment to **5**. Kubernetes creates additional Pods to match the desired state.

---

### Scale Down

```bash
kubectl scale deployment html-deploy --replicas=2
```

**Explanation:**
Reduces the number of running Pod replicas to **2**. Kubernetes removes the extra Pods while maintaining application availability.

---

### Check Deployment Status

```bash
kubectl get deployments
```

**Explanation:**
Displays the Deployment along with the desired, current, and available number of replicas.

---

### List Running Pods

```bash
kubectl get pods
```

**Explanation:**
Shows all Pods created by the Deployment and their current status.

---

### Describe Deployment

```bash
kubectl describe deployment html-deploy
```

**Explanation:**
Provides detailed information about the Deployment, including replicas, events, labels, selectors, and container configuration.

---

### Delete Deployment

```bash
kubectl delete deployment html-deploy
```

**Explanation:**
Deletes the Deployment and all Pods managed by it.

---


