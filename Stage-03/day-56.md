## Day 56: Deploy Nginx Web Server on Kubernetes Cluster

**Challenge:** Deploy an Nginx web server using a Kubernetes Deployment and expose it via a NodePort Service.

---

### Steps Followed

#### 1. Create Deployment Manifest
```bash
vi nginx-deployment.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
```

Apply the deployment:
```bash
kubectl apply -f nginx-deployment.yaml
```

Verify replicas and Pods:
```bash
kubectl get deployment nginx-deployment
kubectl get pods
```

---

#### 2. Create NodePort Service Manifest
```bash
vi nginx-service.yaml
```

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30011
```

Apply the service:
```bash
kubectl apply -f nginx-service.yaml
```

---

#### 3. Verify the Service
```bash
kubectl get svc nginx-service
```

**Expected Output:**
- Service Type: **NodePort**
- Port Mapping: **80:30011/TCP**

---

### Result & Insights
✅ Successfully deployed an **Nginx Deployment** with **3 replicas**.  
✅ Exposed the application externally using a **NodePort Service**.  
💡 Learned how to combine **Deployments** and **Services** to run and access scalable web applications in Kubernet
