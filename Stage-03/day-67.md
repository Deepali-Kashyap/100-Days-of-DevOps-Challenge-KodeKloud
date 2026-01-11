## Day 67: Deploy Guest Book App on Kubernetes

### Task Summary
Deploy the **Guest Book application** on a Kubernetes cluster using a **three-tier architecture**:
- **Backend**: Redis Master
- **Backend**: Redis Slaves
- **Frontend**: PHP-based Guestbook UI exposed via NodePort

This setup demonstrates multi-tier application deployment, service discovery using labels/selectors, and frontend exposure.

---

### Backend Tier

#### Step 1: Redis Master (Deployment + Service)

Create the manifest:
```bash
vi redis-master.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
      role: master
  template:
    metadata:
      labels:
        app: redis
        role: master
    spec:
      containers:
        - name: master-redis-xfusion
          image: redis
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: "100m"
              memory: "100Mi"
---
apiVersion: v1
kind: Service
metadata:
  name: redis-master
spec:
  selector:
    app: redis
    role: master
  ports:
    - port: 6379
      targetPort: 6379
```

Apply:
```bash
kubectl apply -f redis-master.yaml
```

---

#### Step 2: Redis Slave (Deployment + Service)

Create the manifest:
```bash
vi redis-slave.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-slave
spec:
  replicas: 2
  selector:
    matchLabels:
      app: redis
      role: slave
  template:
    metadata:
      labels:
        app: redis
        role: slave
    spec:
      containers:
        - name: slave-redis-xfusion
          image: gcr.io/google_samples/gb-redisslave:v3
          env:
            - name: GET_HOSTS_FROM
              value: dns
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: "100m"
              memory: "100Mi"
---
apiVersion: v1
kind: Service
metadata:
  name: redis-slave
spec:
  selector:
    app: redis
    role: slave
  ports:
    - port: 6379
      targetPort: 6379
```

Apply:
```bash
kubectl apply -f redis-slave.yaml
```

---

## Frontend Tier

#### Step 3: Frontend (Deployment + NodePort Service)

Create the manifest:
```bash
vi frontend.yaml
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: guestbook
      tier: frontend
  template:
    metadata:
      labels:
        app: guestbook
        tier: frontend
    spec:
      containers:
        - name: php-redis-xfusion
          image: gcr.io/google-samples/gb-frontend@sha256:a908df8486ff66f2c4daa0d3d8a2fa09846a1fc8efd65649c0109695c7c5cbff
          env:
            - name: GET_HOSTS_FROM
              value: dns
          ports:
            - containerPort: 80
          resources:
            requests:
              cpu: "100m"
              memory: "100Mi"
---
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: NodePort
  selector:
    app: guestbook
    tier: frontend
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30009
```

Apply:
```bash
kubectl apply -f frontend.yaml
```

---

#### Validation Checklist

Verify all resources:

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

Expected:
- Redis master: 1 pod running
- Redis slaves: 2 pods running
- Frontend: 3 pods running
- Frontend service exposed on **NodePort 30009**

---

#### Outcome & Key Learnings
- Successfully deployed a **multi-tier Guest Book application**
- Implemented **Redis master–slave architecture**
- Used Kubernetes **labels and selectors** for service discovery
- Exposed frontend using **NodePort**
- Validated end-to-end application availability on Kubernetes
