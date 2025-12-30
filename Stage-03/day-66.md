## Day 66: Deploy MySQL on Kubernetes

### Task Summary
Deploy a MySQL database on Kubernetes using Persistent Volumes, Secrets, and a NodePort Service to ensure secure configuration and persistent storage.

---

### Step 1: Create Persistent Volume
**File:** `mysql-pv.yaml`
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /mnt/mysql-data
```
---

**Step 2: Create Persistent Volume Claim**

**File**: `mysql-pvc.yaml`
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
```
---

**Step 3: Create Secrets**

**File**: `mysql-secrets.yaml`

```
apiVersion: v1
kind: Secret
metadata:
  name: mysql-root-pass
type: Opaque
stringData:
  password: YUIidhb667
---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-user-pass
type: Opaque
stringData:
  username: kodekloud_sam
  password: TmPcZjtRQx
---
apiVersion: v1
kind: Secret
metadata:
  name: mysql-db-url
type: Opaque
stringData:
  database: kodekloud_db4
```
---

### Step 4: Create MySQL Deployment

**File**: `mysql-deployment.yaml`

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - name: mysql-container
        image: mysql:5.7
        ports:
        - containerPort: 3306
        env:
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-root-pass
              key: password
        - name: MYSQL_DATABASE
          valueFrom:
            secretKeyRef:
              name: mysql-db-url
              key: database
        - name: MYSQL_USER
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-user-pass
              key: password
        volumeMounts:
        - name: mysql-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
```
--- 

### Step 5: Create MySQL Service

**File**: `mysql-service.yaml`

```
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  type: NodePort
  selector:
    app: mysql
  ports:
  - port: 3306
    targetPort: 3306
    nodePort: 30007
```
--- 
### Step 6: Apply All Resources

```
kubectl apply -f mysql-pv.yaml
kubectl apply -f mysql-pvc.yaml
kubectl apply -f mysql-secrets.yaml
kubectl apply -f mysql-deployment.yaml
kubectl apply -f mysql-service.yaml
```

--- 
### Outcome & Key Learnings
- Deployed MySQL securely using Kubernetes Secrets
- Implemented persistent storage with PV and PVC
- Connected MySQL Deployment to persistent volume
- Exposed MySQL using NodePort Service
- Ensured data persistence and secure configuration in Kubernetes
