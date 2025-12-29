## Day 61: Init Containers in Kubernetes

**Goal:** Implement an init container that initializes data before the main container starts.

---

### Deployment Manifest

Create the file `ic-deploy-devops.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-devops
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-devops
  template:
    metadata:
      labels:
        app: ic-devops
    spec:
      initContainers:
        - name: ic-msg-devops
          image: fedora:latest
          command:
            - /bin/bash
            - -c
            - echo Init Done - Welcome to xFusionCorp Industries > /ic/news
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic

      containers:
        - name: ic-main-devops
          image: fedora:latest
          command:
            - /bin/bash
            - -c
            - |
              while true; do
                cat /ic/news;
                sleep 5;
              done
          volumeMounts:
            - name: ic-volume-devops
              mountPath: /ic

      volumes:
        - name: ic-volume-devops
          emptyDir: {}
```

---

### Apply the Deployment
```bash
kubectl apply -f ic-deploy-devops.yaml
```

---

### Verify Deployment and Pod
```bash
kubectl get deployment ic-deploy-devops
kubectl get pods -l app=ic-devops
```

**Expected:**
- Deployment READY: `1/1`
- Pod STATUS: `Running`

---

### Verify Output from Main Container
```bash
kubectl logs -l app=ic-devops
```

**Expected Output (repeated every 5 seconds):**
```
Init Done - Welcome to xFusionCorp Industries
```

---

### Result & Key Learnings
✅ Init container successfully created a file before the main container started.  
✅ Main container continuously reads the initialized file, demonstrating proper **init container usage**.  
💡 Learned how **initContainers** and **emptyDir** volumes work together in Kubernetes.
