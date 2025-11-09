## Day 51: Execute Rolling Updates in Kubernetes

**Challenge:** Perform a rolling update on an existing Kubernetes deployment to update the container image without downtime.

---

### Steps Followed

1. **Check Deployment Details**
   ```bash
   kubectl get deployment nginx-deployment -o yaml | grep "name:"
   ```
   - Confirms the container name (`nginx-container`) within the deployment.

2. **Update the Image**
   ```bash
   kubectl set image deployment/nginx-deployment nginx-container=nginx:1.17
   ```

3. **Monitor the Rollout Status**
   ```bash
   kubectl rollout status deployment/nginx-deployment
   ```

4. **Verify the Image Update**
   ```bash
   kubectl describe deployment nginx-deployment | grep Image:
   ```
---
### Result & Insights
✅ Successfully updated the **nginx-deployment** from the old image to **nginx:1.17** using a rolling update.  
💡 Learned how **Kubernetes rolling updates** ensure zero downtime by gradually replacing old Pods with new ones.
