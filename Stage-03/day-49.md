## Day 49: Deploy Applications with Kubernetes Deployments

**Challenge:** Deploy an application using a Kubernetes Deployment to manage replicas and updates.

---
### Steps Followed

1. **Create a Deployment**
   ```bash
   kubectl create deployment httpd --image=httpd:latest
   ```
   - `httpd` → Deployment name  
   - `--image=httpd:latest` → Uses the latest Apache HTTP server image

2. **Verify the Deployment**
   ```bash
   kubectl get deploy
   ```

---

### Result & Insights
✅ Successfully deployed an **httpd Deployment** in Kubernetes.  
💡 Learned how **Deployments** manage Pods, provide scaling, and handle updates automatically.
