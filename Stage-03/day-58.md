## Day 58: Deploy Grafana on Kubernetes Cluster

**Goal:** Deploy Grafana using a Kubernetes Deployment and expose it via a NodePort Service.

---

### Step 1: Create Grafana Deployment

Create the deployment manifest:
```bash
vi grafana-deployment-nautilus.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-nautilus
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana-container
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000
```

Apply the deployment:
```bash
kubectl apply -f grafana-deployment-nautilus.yaml
```

Verify the pod:
```bash
kubectl get pods
```

**Expected:** Pod status should be `Running`.

---

### Step 2: Create NodePort Service

Create the service manifest:
```bash
vi grafana-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
```

Apply the service:
```bash
kubectl apply -f grafana-service.yaml
```

Verify the service:
```bash
kubectl get svc grafana-service
```

**Expected Output:**
```text
TYPE       NodePort
PORT(S)    3000:32000/TCP
```

---

### Step 3: Access Grafana

---

### Result & Key Learnings
✅ Grafana deployed successfully using a Kubernetes Deployment.  
✅ NodePort service exposed Grafana externally on port `32000`.  
💡 Learned how to deploy and expose monitoring tools in Kubernetes.
