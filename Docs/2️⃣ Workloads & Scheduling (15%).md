

## **🔹 Understanding Kubernetes Workloads**
Kubernetes workloads define how applications run in the cluster. The main types of workloads are:
- **Pods**: The smallest deployable unit, containing one or more containers.
- **ReplicaSets**: Ensure a specified number of identical Pods run at all times.
- **Deployments**: Manage ReplicaSets and provide rolling updates and rollbacks.
- **StatefulSets**: Used for stateful applications requiring stable network identities.
- **DaemonSets**: Ensure a copy of a Pod runs on all (or some) nodes.
- **Jobs & CronJobs**: Run batch tasks and scheduled workloads.

---

## **🔹 Pods & Deployments**
### **1️⃣ Pods**
A **Pod** is the basic unit in Kubernetes that encapsulates a containerized application.

#### **Example: Simple Pod Definition**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: nginx
    image: nginx:latest
```
#### **Useful Commands**
```sh
kubectl get pods
kubectl describe pod my-pod
kubectl logs my-pod
```

### **2️⃣ Deployments**
A **Deployment** provides updates, rollbacks, and scaling.

#### **Example: Creating a Deployment**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: web-app
  template:
    metadata:
      labels:
        app: web-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.21.0
```
#### **Useful Commands**
```sh
kubectl get deployments
kubectl scale deployment web-app --replicas=5
kubectl rollout restart deployment web-app
```

---

## **🔹 ReplicaSets & StatefulSets**
### **3️⃣ ReplicaSets**
ReplicaSets ensure a fixed number of pod replicas are running.

#### **Example: ReplicaSet**
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: nginx
        image: nginx:latest
```
#### **Useful Commands**
```sh
kubectl get replicasets
kubectl delete replicaset my-replicaset
```

### **4️⃣ StatefulSets**
StatefulSets are used for **stateful applications** like databases.

#### **Example: StatefulSet**
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-database
spec:
  replicas: 2
  serviceName: "db-service"
  selector:
    matchLabels:
      app: database
  template:
    metadata:
      labels:
        app: database
    spec:
      containers:
      - name: mysql
        image: mysql:5.7
```
#### **Useful Commands**
```sh
kubectl get statefulsets
kubectl delete statefulset my-database
```

---

## **🔹 DaemonSets & Jobs**
### **5️⃣ DaemonSets**
DaemonSets ensure that **a copy of a Pod runs on all (or specific) nodes**.

#### **Example: DaemonSet**
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: monitoring-agent
spec:
  selector:
    matchLabels:
      app: monitoring-agent
  template:
    metadata:
      labels:
        app: monitoring-agent
    spec:
      containers:
      - name: prometheus
        image: prom/node-exporter
```
#### **Useful Commands**
```sh
kubectl get daemonsets
kubectl delete daemonset monitoring-agent
```

### **6️⃣ Jobs & CronJobs**
Jobs and CronJobs handle batch processing tasks.

#### **Example: Job**
```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: batch-job
spec:
  template:
    spec:
      containers:
      - name: job
        image: busybox
        command: ["/bin/sh", "-c", "echo Hello Kubernetes!"]
      restartPolicy: Never
```
#### **Example: CronJob**
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: scheduled-task
spec:
  schedule: "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron
            image: busybox
            command: ["/bin/sh", "-c", "echo Running scheduled task"]
          restartPolicy: OnFailure
```
#### **Useful Commands**
```sh
kubectl get jobs
kubectl get cronjobs
kubectl delete cronjob scheduled-task
```

---

## **🔹 Pod Scheduling & Node Selection**
Kubernetes allows fine-grained control over **where Pods are scheduled**.

### **7️⃣ Node Affinity & Taints/Tolerations**
- **Node Affinity** ensures that Pods are scheduled on specific nodes.
- **Taints & Tolerations** prevent certain Pods from running on specific nodes.

#### **Example: Node Affinity**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: affinity-pod
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd
  containers:
  - name: app
    image: nginx
```
#### **Useful Commands**
```sh
kubectl describe nodes | grep Taints
kubectl taint nodes node1 key=value:NoSchedule
```

---

## **✅ Summary**
- **Deployments** manage rolling updates and scaling.
- **ReplicaSets** maintain a desired number of identical Pods.
- **StatefulSets** provide stable network identities for stateful applications.
- **DaemonSets** ensure Pods run on all (or selected) nodes.
- **Jobs & CronJobs** handle batch and scheduled workloads.
- **Node Affinity & Taints/Tolerations** control Pod scheduling.

---

[**🚀 Next Topic: Services & Networking**][obsidian://open?vault=Toyota&file=Personal%2FCKA%2F3%EF%B8%8F%E2%83%A3%20Services%20%26%20Networking%20(20%25)]

