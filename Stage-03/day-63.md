## Day 63: Deploy Iron Gallery App on Kubernetes

### Objective
Deploy the **Iron Gallery application** and its **MariaDB backend** inside a dedicated Kubernetes namespace using Deployments and Services.


### Step 1: Create Namespace

```bash
kubectl create namespace iron-namespace-xfusion
kubectl get namespace iron-namespace-xfusion
```

---

### Step 2: Iron Gallery Deployment

**File:** `iron-gallery-deployment-xfusion.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-gallery-deployment-xfusion
  namespace: iron-namespace-xfusion
spec:
  replicas: 1
  selector:
    matchLabels:
      run: iron-gallery
  template:
    metadata:
      labels:
        run: iron-gallery
    spec:
      containers:
        - name: iron-gallery-container-xfusion
          image: kodekloud/irongallery:2.0
          resources:
            limits:
              memory: 100Mi
              cpu: 50m
          volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/data
            - name: images
              mountPath: /usr/share/nginx/html/uploads
      volumes:
        - name: config
          emptyDir: {}
        - name: images
          emptyDir: {}
```

Apply:
```bash
kubectl apply -f iron-gallery-deployment-xfusion.yaml
```

---

### Step 3: Iron DB Deployment

**File:** `iron-db-deployment-xfusion.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-db-deployment-xfusion
  namespace: iron-namespace-xfusion
spec:
  replicas: 1
  selector:
    matchLabels:
      db: mariadb
  template:
    metadata:
      labels:
        db: mariadb
    spec:
      containers:
        - name: iron-db-container-xfusion
          image: kodekloud/irondb:2.0
          env:
            - name: MYSQL_DATABASE
              value: database_host
            - name: MYSQL_ROOT_PASSWORD
              value: R00t@StrongPass!23
            - name: MYSQL_PASSWORD
              value: User@StrongPass!23
            - name: MYSQL_USER
              value: ironuser
          volumeMounts:
            - name: db
              mountPath: /var/lib/mysql
      volumes:
        - name: db
          emptyDir: {}
```

Apply:
```bash
kubectl apply -f iron-db-deployment-xfusion.yaml
```

---

### Step 4: Iron DB Service (ClusterIP)

**File:** `iron-db-service-xfusion.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: iron-db-service-xfusion
  namespace: iron-namespace-xfusion
spec:
  selector:
    db: mariadb
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
  type: ClusterIP
```

Apply:
```bash
kubectl apply -f iron-db-service-xfusion.yaml
```

---

### Step 5: Iron Gallery Service (NodePort)

**File:** `iron-gallery-service-xfusion.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: iron-gallery-service-xfusion
  namespace: iron-namespace-xfusion
spec:
  selector:
    run: iron-gallery
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 32678
  type: NodePort
```

Apply:
```bash
kubectl apply -f iron-gallery-service-xfusion.yaml
```

---

### Step 6: Final Verification

```bash
kubectl get all -n iron-namespace-xfusion
```

**Expected:**
- Both Deployments: `READY 1/1`
- Pods: `Running`
- Services: `ClusterIP` and `NodePort` created successfully

---

### Outcome & Key Learnings

✅ Deployed a multi-tier application using Kubernetes  
✅ Used a dedicated namespace for isolation  
✅ Implemented resource limits and emptyDir volumes  
✅ Exposed frontend using NodePort and backend using ClusterIP  

This setup satisfies all task validation requirements and is production-aligned for namespace-scoped deployments.
