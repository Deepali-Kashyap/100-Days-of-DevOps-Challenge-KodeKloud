## Day 54: Kubernetes Shared Volumes

**Challenge:** Demonstrate shared storage between multiple containers in a single Pod using an `emptyDir` volume.

---

### Steps Followed

### 1. Create Pod Manifest (emptyDir Shared Volume)
```bash
vi volume-share-xfusion.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-xfusion
spec:
  volumes:
    - name: volume-share
      emptyDir: {}
  containers:
    - name: volume-container-xfusion-1
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/beta

    - name: volume-container-xfusion-2
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/demo
```

Apply the manifest:
```bash
kubectl apply -f volume-share-xfusion.yaml
```

Verify the Pod:
```bash
kubectl get pod volume-share-xfusion
```

---

### 2. Create a File in the First Container
```bash
kubectl exec -it volume-share-xfusion -c volume-container-xfusion-1 -- bash
```

Inside the container:
```bash
echo "Shared volume test file" > /tmp/beta/beta.txt
exit
```

---

### 3. Verify the File in the Second Container
```bash
kubectl exec -it volume-share-xfusion -c volume-container-xfusion-2 -- bash
ls /tmp/demo
cat /tmp/demo/beta.txt
```

---

### Result & Insights
✅ Verified that a file created in **container 1** is accessible in **container 2** via the shared `emptyDir` volume.  
💡 Learned how **emptyDir volumes** enable fast, temporary data sharing between containers within the same Pod.
