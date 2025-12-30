## Day 64: Fix Python App Deployed on Kubernetes Cluster

### Objective
Resolve misconfigurations in a Python Flask app deployment so it becomes accessible via the specified NodePort.

We made two changes:  
1. Corrected the image name from `poroko/flask-app-demo` → `poroko/flask-demo-app`  
2. Corrected the Service target port from `8080` → `5000`

Apply changes by editing deployment and service:

```bash
kubectl edit deployment python-deployment-datacenter
kubectl edit svc python-service-datacenter
```

---

### Issues Identified

1. **Image Pull Error** – Deployment was using a non-existent image:

```yaml
image: poroko/flask-app-demo
```

**Correct image:**

```yaml
image: poroko/flask-demo-app
```

2. **Service Target Port Mismatch** – Service was forwarding traffic to the wrong container port:

```yaml
targetPort: 8080
```

**Correct targetPort:**

```yaml
targetPort: 5000
```

---

### Verification Steps

1. Check that the pod is running:

```bash
kubectl get pods --show-labels
```

2. Check that the Service has correct endpoints:

```bash
kubectl get endpoints python-service-datacenter
```

**Expected output:**

```
ENDPOINTS: <Pod-IP>:5000
```

### Outcome & Key Learnings

- Corrected deployment image to ensure successful pull  
- Fixed Service target port to properly route traffic to container  
- Verified pod readiness and Service endpoints  
- Flask app now accessible via NodePort as intended  
