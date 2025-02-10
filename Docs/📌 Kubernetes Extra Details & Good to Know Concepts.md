

## **🔹 General Kubernetes Concepts**
- **Kubernetes follows a declarative approach**: You define the desired state in YAML/JSON, and Kubernetes ensures it is maintained.
- **Immutable Infrastructure**: Instead of modifying running containers, update Deployments and roll out changes.
- **Kubernetes Objects** (Pods, Deployments, Services, etc.) follow a **desired state vs. actual state** model.

### **Understanding API Groups & Versions**
- Kubernetes API resources are grouped into different API groups.
- Example:
  - `v1` (Core API) – Pods, Services, ConfigMaps, Secrets.
  - `apps/v1` – Deployments, StatefulSets, ReplicaSets.
  - `batch/v1` – Jobs, CronJobs.
  - `networking.k8s.io/v1` – Ingress, NetworkPolicies.
- Use `kubectl api-resources` to list available resources.

---

## **🔹 Workloads & Scheduling Details**
### **Pods & Container Best Practices**
- Always **set resource requests and limits** to prevent resource starvation:
  ```yaml
  resources:
    requests:
      cpu: "250m"
      memory: "256Mi"
    limits:
      cpu: "500m"
      memory: "512Mi"
  ```
- Use **readiness probes** to prevent traffic from reaching unready pods:
  ```yaml
  readinessProbe:
    httpGet:
      path: /healthz
      port: 8080
    initialDelaySeconds: 5
    periodSeconds: 10
  ```
- Use **liveness probes** to restart crashed applications:
  ```yaml
  livenessProbe:
    exec:
      command: ["cat", "/tmp/healthy"]
    initialDelaySeconds: 5
    periodSeconds: 10
  ```

### **DaemonSets Best Practices**
- Use DaemonSets for **node-wide services** like logging, monitoring, and networking plugins.
- Ensure proper **taints and tolerations** so that DaemonSets don’t run on master nodes unnecessarily.
  ```yaml
  tolerations:
    - key: "node-role.kubernetes.io/master"
      operator: "Exists"
      effect: "NoSchedule"
  ```

### **StatefulSets Key Considerations**
- Pods in StatefulSets get stable hostnames (`pod-0`, `pod-1`).
- Good for databases like MySQL, PostgreSQL, and distributed systems like Kafka.
- Ensure proper **PVC templates** so each Pod gets persistent storage.

---

## **🔹 Networking Deep Dive**
### **Service Discovery & Networking**
- Every Service in Kubernetes gets a **DNS entry** (`my-service.my-namespace.svc.cluster.local`).
- Services use **endpoints** to route traffic to correct Pods.
  ```sh
  kubectl get endpoints my-service
  ```
- **LoadBalancer Services** require cloud integration (e.g., AWS ELB, Azure LB).
- Use `kubectl port-forward` for local testing:
  ```sh
  kubectl port-forward svc/my-service 8080:80
  ```

### **Ingress Controllers & TLS**
- Use Ingress for **path-based or host-based routing**.
- Example NGINX Ingress with TLS:
  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: Ingress
  metadata:
    name: web-ingress
  spec:
    tls:
    - hosts:
      - example.com
      secretName: tls-secret
    rules:
    - host: example.com
      http:
        paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: web-service
              port:
                number: 80
  ```
- Generate a TLS Secret for Ingress:
  ```sh
  kubectl create secret tls tls-secret --cert=cert.pem --key=key.pem
  ```

---

## **🔹 Storage Advanced Concepts**
### **Dynamic Storage Provisioning**
- Use **StorageClasses** to dynamically provision PVs.
- Example StorageClass for AWS EBS:
  ```yaml
  apiVersion: storage.k8s.io/v1
  kind: StorageClass
  metadata:
    name: gp2-storage
  provisioner: kubernetes.io/aws-ebs
  parameters:
    type: gp2
  reclaimPolicy: Delete
  ```

### **NFS & Shared Storage**
- Use **NFS Persistent Volumes** for shared storage across multiple Pods.
  ```yaml
  apiVersion: v1
  kind: PersistentVolume
  metadata:
    name: nfs-pv
  spec:
    capacity:
      storage: 10Gi
    accessModes:
      - ReadWriteMany
    nfs:
      path: /mnt/data
      server: 192.168.1.100
  ```

---

## **🔹 Security Best Practices**
### **RBAC (Role-Based Access Control)**
- Use **Roles** and **RoleBindings** to limit permissions.
- Example Role allowing only `get` and `list` for Pods:
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: Role
  metadata:
    namespace: default
    name: pod-reader
  rules:
  - apiGroups: [""]
    resources: ["pods"]
    verbs: ["get", "list"]
  ```
- Bind Role to a user:
  ```yaml
  apiVersion: rbac.authorization.k8s.io/v1
  kind: RoleBinding
  metadata:
    name: read-pods-binding
    namespace: default
  subjects:
  - kind: User
    name: jane
    apiGroup: rbac.authorization.k8s.io
  roleRef:
    kind: Role
    name: pod-reader
    apiGroup: rbac.authorization.k8s.io
  ```

### **Pod Security Contexts**
- Run Pods with **non-root users** to improve security.
  ```yaml
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  ```
- Restrict container capabilities:
  ```yaml
  securityContext:
    capabilities:
      drop:
      - ALL
  ```

---

## **✅ Summary**
- **Master API Groups** (`v1`, `apps/v1`, `batch/v1`, etc.).
- **Use resource limits, probes, and RBAC** for better security & reliability.
- **Leverage StorageClasses & StatefulSets** for stateful applications.
- **Optimize Ingress & networking settings** for production traffic.
- **Secure Pods with SecurityContexts & RoleBindings**.



