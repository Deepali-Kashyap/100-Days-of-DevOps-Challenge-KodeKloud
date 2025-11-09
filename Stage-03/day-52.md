## Day 52: Revert Deployment to Previous Version in Kubernetes

**Challenge:** Roll back a Kubernetes Deployment to its previous working version after a recent update.

---

### Steps Followed

1. **Check Deployment Revision History**
   ```bash
   kubectl rollout history deployment/nginx-deployment
   ```

2. **Revert to the Previous Version**
   ```bash
   kubectl rollout undo deployment/nginx-deployment
   ```
   ✅ Output:
   ```
   deployment.apps/nginx-deployment rolled back
   ```

3. **Verify the Rollback Status**
   ```bash
   kubectl rollout status deployment/nginx-deployment
   ```
   ✅ Output:
   ```
   deployment "nginx-deployment" successfully rolled out
   ```

---
### Result & Insights
✅ Successfully rolled back the **nginx-deployment** to its previous version.  
💡 Learned how to **view deployment history**, **undo faulty updates**, and **restore stable releases** seamlessly in Kubernetes.
