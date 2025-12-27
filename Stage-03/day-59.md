## Day 59: Troubleshoot Deployment Issues in Kubernetes

**Goal:** Fix deployment issues by updating the container name, image, and removing volume mounts.

---

### Step 1: Edit the Deployment

Edit the existing deployment:
```bash
kubectl edit deployment <deployment-name>
```

---

### Step 2: Apply Required Fixes

Make the following changes in the container spec:

- **Change container name**
- **Update image to `redis:latest`**
- **Remove all `volumeMounts` and related `volumes`**

### Example (Corrected Container Section):
```yaml
containers:
  - name: redis-container
    image: redis:latest
```

Ensure there are **no `volumeMounts:` or `volumes:` entries** in the deployment.

---

### Step 3: Save and Verify

After saving, Kubernetes will automatically apply the changes.

Check deployment and pods:
```bash
kubectl get deployment
kubectl get pods
```

---

### Result & Key Learnings
✅ Deployment updated successfully with the correct container name and image.  
✅ Removing invalid volume mounts resolved deployment issues.  
💡 Learned how to troubleshoot and fix common Kubernetes deployment misconfigurations.
