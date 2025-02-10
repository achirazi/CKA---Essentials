

## **🔹 Understanding Kubernetes Storage**
Storage in Kubernetes ensures **data persistence** for applications running in Pods. Kubernetes provides multiple storage options:

- **Ephemeral Storage** (Temporary storage inside Pods)
- **Persistent Storage** (Survives Pod restarts)
- **Persistent Volumes (PV) & Persistent Volume Claims (PVC)**
- **Storage Classes** for dynamic provisioning

---

## **🔹 Ephemeral Storage**
### **1️⃣ EmptyDir**
- **Data is lost when the Pod is deleted**.
- **Useful for caching or temporary file storage**.

#### **Example: EmptyDir Volume**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ephemeral-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
    volumeMounts:
    - mountPath: /cache
      name: temp-storage
  volumes:
  - name: temp-storage
    emptyDir: {}
```
#### **Useful Commands**
```sh
kubectl get pods ephemeral-pod -o yaml
```

---

## **🔹 Persistent Volumes (PVs) & Persistent Volume Claims (PVCs)**
### **2️⃣ Persistent Volumes (PVs)**
A **Persistent Volume (PV)** is **pre-provisioned storage** in Kubernetes.

#### **Example: Persistent Volume (PV)**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /mnt/data
```

### **3️⃣ Persistent Volume Claims (PVCs)**
A **Persistent Volume Claim (PVC)** requests storage from a PV.

#### **Example: Persistent Volume Claim (PVC)**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 10Gi
```
#### **Useful Commands**
```sh
kubectl get pv
kubectl get pvc
kubectl describe pvc my-pvc
```

---

## **🔹 Storage Classes & Dynamic Provisioning**
### **4️⃣ Storage Classes**
A **StorageClass** allows Kubernetes to dynamically provision PVs based on user requests.

#### **Example: StorageClass for Dynamic Provisioning**
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Delete
```

#### **Using the StorageClass in a PVC**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: fast-storage
```
#### **Useful Commands**
```sh
kubectl get storageclass
kubectl describe storageclass fast-storage
```

---

## **🔹 Volume Types in Kubernetes**
### **5️⃣ Common Volume Types**
| Volume Type | Description |
|------------|-------------|
| **emptyDir** | Temporary storage inside a Pod (deleted with Pod) |
| **hostPath** | Uses a folder from the node’s filesystem |
| **Persistent Volume (PV)** | Persistent storage managed by Kubernetes |
| **NFS** | Network-based storage (useful for shared volumes) |
| **AWS EBS, GCE PD, Azure Disk** | Cloud-based storage |

#### **Example: hostPath Volume**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hostpath-pod
spec:
  containers:
  - name: busybox
    image: busybox
    volumeMounts:
    - mountPath: /data
      name: my-volume
  volumes:
  - name: my-volume
    hostPath:
      path: /data
```
#### **Useful Commands**
```sh
kubectl get pods hostpath-pod -o yaml
```

---

## **🔹 Backup & Restore PVCs**
### **6️⃣ Backing Up a Persistent Volume**
```sh
kubectl cp my-pod:/data /backup/
```

### **7️⃣ Restoring a Persistent Volume**
```sh
kubectl cp /backup/ my-pod:/data
```

---

## **✅ Summary**
- **EmptyDir** provides temporary storage inside Pods.
- **Persistent Volumes (PVs)** are pre-provisioned storage.
- **Persistent Volume Claims (PVCs)** request storage from PVs.
- **Storage Classes** enable dynamic volume provisioning.
- **Different volume types (hostPath, NFS, cloud storage)** cater to various needs.

---

[ **🚀 Next Topic: Troubleshooting**][obsidian://open?vault=Toyota&file=Personal%2FCKA%2F5%EF%B8%8F%E2%83%A3%20Troubleshooting%20(30%25)]

