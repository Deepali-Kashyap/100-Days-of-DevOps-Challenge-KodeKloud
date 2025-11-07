## Day 48: Deploy Pods in Kubernetes Cluster

**Challenge:** Deploy a single Pod in a Kubernetes cluster running the Apache HTTP server.

---

### Steps Followed

1. **Create Pod Definition File**
   ```bash
   vi pod-httpd.yaml
   ```

2. **Add the Following Content**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: pod-httpd
     labels:
       app: httpd_app
   spec:
     containers:
     - name: httpd-container
       image: httpd:latest
   ```

3. **Deploy the Pod**
   ```bash
   kubectl apply -f pod-httpd.yaml
   ```

4. **Verify the Pod**
   ```bash
   kubectl get pods
   ```

---
### Result & Insights
✅ Successfully deployed a **Pod** named `pod-httpd` running **httpd:latest**.  
💡 Learned the basics of **Pod creation** using YAML and verifying resources in Kubernetes.
