## Day 53: Resolve VolumeMounts Issue in Kubernetes

**Challenge:** Fix an incorrect volume mount path in a running Kubernetes Pod and validate the application after correction.

---

### Steps Followed

1. **Check Running Pods**
   ```bash
   kubectl get pods
   ```

2. **Inspect Existing ConfigMap**
   ```bash
   kubectl get configmap
   kubectl describe configmap nginx-config
   ```

3. **Export Pod Configuration**
   ```bash
   kubectl get pod nginx-phpfpm -o yaml > /tmp/nginx.yaml
   cat /tmp/nginx.yaml
   ```

4. **Update the Volume Mount Path**
   - Identify the old path:
     ```bash
     cat /tmp/nginx.yaml | grep /usr/share/nginx/html
     ```
   - Edit the file and change:
     ```
     /usr/share/nginx/html → /var/www/html
     ```
     ```bash
     vim /tmp/nginx.yaml
     ```

5. **Replace the Running Pod**
   ```bash
   kubectl replace -f /tmp/nginx.yaml --force
   ```

6. **Wait for Pod to Reach Running State**
   ```bash
   kubectl get pods
   ```

7. **Copy Application File into the Pod**
   ```bash
   kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html -c nginx-container
   ```

8. **Validate the Fix**
   ```bash
   kubectl exec -it nginx-phpfpm -c nginx-container -- curl -I http://localhost:8099
   ```

---
### Result & Insights
✅ Corrected the volume mount path and successfully replaced the running Pod.  
💡 Learned how to **export, modify, and reapply Pod configurations** to resolve VolumeMount issues and validate application availability.
