## Day 50: Set Resource Limits in Kubernetes Pods

**Challenge:** Define and apply CPU and memory resource requests and limits for a Kubernetes Pod.

---

## Steps Followed

1. **Create Pod Manifest File**
   ```bash
   vi pods.yaml
   ```

2. **Add the Following Content**
   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: httpd-pod
   spec:
     containers:
       - name: httpd-container
         image: httpd:latest
         resources:
           requests:
             memory: "15Mi"
             cpu: "100m"
           limits:
             memory: "20Mi"
             cpu: "100m"
   ```

3. **Apply the Manifest**
   ```bash
   kubectl apply -f pods.yaml
   ```

4. **Verify the Pod**
   ```bash
   kubectl get pods
   ```

---
### Result & Insights
✅ Successfully created a Pod with **CPU and memory requests and limits**.  
💡 Learned how to manage resource allocation in Kubernetes to ensure Pods do not exceed defined capacities and get scheduled efficiently.
