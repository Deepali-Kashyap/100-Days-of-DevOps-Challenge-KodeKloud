## Day 57: Print Environment Variables

**Goal:** Create a Kubernetes Pod that prints environment variables and exits successfully.

---

### Pod Manifest
Create the file:
```bash
vi print-envars-greeting.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  restartPolicy: Never
  containers:
    - name: print-env-container
      image: bash:latest
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "DevOps"
        - name: GROUP
          value: "Ltd"
      command:
        - /bin/sh
        - -c
        - echo "$(GREETING) $(COMPANY) $(GROUP)"
```

---

### Create the Pod
```bash
kubectl apply -f print-envars-greeting.yaml
```

---

### Verify Pod Status
```bash
kubectl get pod print-envars-greeting
```

**Expected Status:** `Completed`

---

### Check Output
```bash
kubectl logs -f print-envars-greeting
```

**Expected Output:**
```text
Welcome to DevOps Ltd
```

---

### Result & Key Learnings
✅ Environment variables were injected into the container successfully.  
✅ The container executed the command and exited cleanly (`restartPolicy: Never`).  
💡 Learned how to define and consume environment variables in a Kubernetes Pod.
