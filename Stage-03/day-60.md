## Day 60: Persistent Volumes in Kubernetes

**Goal:** Configure PersistentVolume (PV), PersistentVolumeClaim (PVC), mount it to a Pod, and expose via NodePort Service.

---

### 1️⃣ Create PersistentVolume (PV)

**pv-devops.yaml**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-devops
spec:
  storageClassName: manual
  capacity:
    storage: 4Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/sysops
```

```bash
kubectl apply -f pv-devops.yaml
```

---

### 2️⃣ Create PersistentVolumeClaim (PVC)

**pvc-devops.yaml**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-devops
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```

```bash
kubectl apply -f pvc-devops.yaml
kubectl get pv,pvc
```

✅ **Expected:** PV and PVC status → `Bound`

---

### 3️⃣ Create Pod Using PVC

**pod-devops.yaml**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-devops
  labels:
    app: web-devops
spec:
  containers:
    - name: container-devops
      image: nginx:latest
      ports:
        - containerPort: 80
      volumeMounts:
        - name: web-storage
          mountPath: /usr/share/nginx/html
  volumes:
    - name: web-storage
      persistentVolumeClaim:
        claimName: pvc-devops
```

```bash
kubectl apply -f pod-devops.yaml
kubectl get pod pod-devops
```

---

### 4️⃣ Create NodePort Service

**web-devops.yaml**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: web-devops
spec:
  type: NodePort
  selector:
    app: web-devops
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

```bash
kubectl apply -f web-devops.yaml
kubectl get svc web-devops
```

---

### 5️⃣ Access the Application

```bash
kubectl get nodes -o wide
```


---

### ✅ Outcome & Key Learnings

- Successfully configured **PV → PVC → Pod** binding
- Persistent storage mounted at **/usr/share/nginx/html**
- Application exposed using **NodePort**
- Learned how Kubernetes handles persistent data using hostPath volumes
