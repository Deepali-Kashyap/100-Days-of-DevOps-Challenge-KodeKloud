## Day 55: Kubernetes Sidecar Containers

**Challenge:** Implement a sidecar container pattern to share and process logs from a main application container using a shared volume.

---

### Steps Followed

### 1. Create Pod Manifest
```bash
vi webserver.yaml
```

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}

  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx

    - name: sidecar-container
      image: ubuntu:latest
      command:
        - sh
        - -c
        - |
          while true; do
            cat /var/log/nginx/access.log /var/log/nginx/error.log;
            sleep 30;
          done
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```

---

### 2. Deploy the Pod
```bash
kubectl apply -f webserver.yaml
```

### 3. Verify Pod Status
```bash
kubectl get pod webserver
kubectl describe pod webserver
```
- Pod status should be **Running**
- Both containers should be active without restarts

---

### 4. Validate Log Sharing (Optional)

Generate traffic:
```bash
kubectl exec -it webserver -c nginx-container -- curl localhost
```

Check logs from sidecar:
```bash
kubectl logs webserver -c sidecar-container
```

---

## Result & Insights
✅ Successfully implemented a **sidecar container pattern** using a shared `emptyDir` volume.  
💡 Learned how sidecar containers can **consume logs or data** from a main container in real time, a common pattern for logging, monitoring, and data processing in Kubernetes.
