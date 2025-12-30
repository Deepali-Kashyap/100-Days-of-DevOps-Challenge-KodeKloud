## Day 65: Deploy Redis Deployment on Kubernetes

### Task Summary
Deploy a Redis application on Kubernetes using a Deployment with the following requirements:
- Use a ConfigMap to inject Redis configuration (`maxmemory 2mb`)
- Deploy Redis using the `redis:alpine` image
- Configure container resources (CPU request)
- Use `emptyDir` for data storage
- Mount the ConfigMap into the container
- Expose Redis on port `6379`
- Ensure the Deployment and Pod are in a Running state

---

### Step 1: Create the ConfigMap (Imperative)

Create a ConfigMap named `my-redis-config` with Redis configuration:

```bash
kubectl create configmap my-redis-config \
  --from-literal=redis-config="maxmemory 2mb"
```

Verify the ConfigMap:

```bash
kubectl get configmap my-redis-config -o yaml
```

---

### Step 2: Generate Deployment YAML (Dry Run)

Generate a base Deployment manifest and save it to a file:

```bash
kubectl create deployment redis-deployment \
  --image=redis:alpine \
  --replicas=1 \
  --dry-run=client -o yaml > redis-deployment.yaml
```

---

### Step 3: Edit the Deployment Manifest

Update `redis-deployment.yaml` with the required configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-deployment
  template:
    metadata:
      labels:
        app: redis-deployment
    spec:
      containers:
        - name: redis-container
          image: redis:alpine
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: "1"
          volumeMounts:
            - name: data
              mountPath: /redis-master-data
            - name: redis-config
              mountPath: /redis-master
      volumes:
        - name: data
          emptyDir: {}
        - name: redis-config
          configMap:
            name: my-redis-config
```

---

### Step 4: Apply the Deployment

```bash
kubectl apply -f redis-deployment.yaml
```

---

### Step 5: Verify Deployment Status

Check the Deployment and Pod status:

```bash
kubectl get deployment redis-deployment
kubectl get pods -l app=redis-deployment
```

Optional detailed inspection:

```bash
kubectl describe pod -l app=redis-deployment
```

---

### Outcome & Key Learnings
- Successfully deployed Redis using a Kubernetes Deployment  
- Used a ConfigMap to externalize Redis configuration  
- Applied CPU resource requests for predictable scheduling  
- Mounted both configuration and data using volumes  
- Validated Deployment and Pod health using standard Kubernetes commands  
