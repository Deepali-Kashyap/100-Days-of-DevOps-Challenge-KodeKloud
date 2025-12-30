## Day 62: Manage Secrets in Kubernetes

**Goal:** Create a Kubernetes Secret from a file and mount it inside a Pod.


### Task Summary

- A file `blog.txt` already exists at `/opt/blog.txt` on the jump host  
- Create a **generic secret** named `blog` using this file  
- Create a Pod named `secret-nautilus`  
- Mount the secret inside the container at `/opt/cluster`  
- Verify the secret content inside the container  

---

### Step 1: Create the Secret from File

```bash
kubectl create secret generic blog --from-file=/opt/blog.txt
```

Verify the secret:

```bash
kubectl get secret blog
```

---

### Step 2: Create the Pod Manifest

Create the file `secret-nautilus.yaml`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-nautilus
spec:
  containers:
    - name: secret-container-nautilus
      image: fedora:latest
      command:
        - sleep
        - "3600"
      volumeMounts:
        - name: blog-secret
          mountPath: /opt/cluster
          readOnly: true
  volumes:
    - name: blog-secret
      secret:
        secretName: blog
```

---

### Step 3: Apply the Pod

```bash
kubectl apply -f secret-nautilus.yaml
```

Verify Pod status:

```bash
kubectl get pod secret-nautilus
```

**Expected:** `Running (1/1)`

---

### Step 4: Verify the Secret Inside the Container

Access the container:

```bash
kubectl exec -it secret-nautilus -- bash
```

Check the mounted secret:

```bash
ls /opt/cluster
cat /opt/cluster/blog.txt
```

You should see the content stored in `blog.txt`.

---

### Result & Key Learnings

✅ Created a Kubernetes Secret from an existing file  
✅ Mounted the secret securely inside a Pod  
✅ Verified secret data from within the container  

💡 Learned how Kubernetes Secrets can be consumed as **read-only volumes** for secure configuration management.
