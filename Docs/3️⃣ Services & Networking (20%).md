
## **🔹 Understanding Kubernetes Networking**
Kubernetes networking ensures **communication between Pods, Services, and external users**.

- **Pod-to-Pod Communication**: Pods communicate using their IP addresses inside the cluster.
- **Service-to-Pod Communication**: Services provide stable networking for Pods.
- **External Access**: Ingress and LoadBalancers expose applications to external users.
- **Network Policies**: Restrict traffic between Pods based on rules.

---

## **🔹 Service Types in Kubernetes**
A **Service** is an abstraction that exposes a set of Pods as a **network-accessible endpoint**.

### **1️⃣ ClusterIP (Default Service)**
- Exposes the service **internally** within the cluster.
- **Not accessible from outside** the cluster.

#### **Example: ClusterIP Service**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-clusterip-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP
```
#### **Useful Commands**
```sh
kubectl get svc
kubectl describe svc my-clusterip-service
```

---

### **2️⃣ NodePort Service**
- Exposes the service on **a static port on each node’s IP**.
- **Accessible externally** via `<NodeIP>:<NodePort>`.

#### **Example: NodePort Service**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
      nodePort: 30007
  type: NodePort
```
#### **Useful Commands**
```sh
kubectl get svc
kubectl describe svc my-nodeport-service
```

---

### **3️⃣ LoadBalancer Service**
- Creates an **external LoadBalancer** using a cloud provider (AWS, GCP, Azure).
- **Recommended for production** when using cloud environments.

#### **Example: LoadBalancer Service**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer
```
#### **Useful Commands**
```sh
kubectl get svc
kubectl describe svc my-loadbalancer-service
```

---

### **4️⃣ ExternalName Service**
- Maps a Kubernetes Service to an **external DNS hostname**.
- Useful for integrating with **external APIs or databases**.

#### **Example: ExternalName Service**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-external-service
spec:
  type: ExternalName
  externalName: api.example.com
```
#### **Useful Commands**
```sh
kubectl get svc
kubectl describe svc my-external-service
```

---

## **🔹 Ingress for HTTP/HTTPS Traffic**
An **Ingress** exposes HTTP(S) routes to services using an **Ingress Controller** (NGINX, Traefik, etc.).

### **Example: Ingress Resource**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```
#### **Useful Commands**
```sh
kubectl get ingress
kubectl describe ingress my-ingress
```

---

## **🔹 Network Policies**
Network Policies **restrict or allow communication** between Pods.

### **Example: Deny All Traffic Policy**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector:
    matchLabels:
      app: my-app
  policyTypes:
  - Ingress
  - Egress
```
#### **Useful Commands**
```sh
kubectl get networkpolicy
kubectl describe networkpolicy deny-all
```

---

## **🔹 CoreDNS & Debugging DNS**
### **Check DNS Resolution Inside a Pod**
```sh
kubectl run dns-test --image=busybox --rm -it -- nslookup my-service
```

### **Check CoreDNS Logs**
```sh
kubectl logs -n kube-system -l k8s-app=kube-dns
```

---

## **✅ Summary**
- **ClusterIP** is for internal communication.
- **NodePort** exposes services on each node.
- **LoadBalancer** provides external access via cloud providers.
- **Ingress** manages HTTP/S routing.
- **Network Policies** control inter-Pod communication.
- **CoreDNS** provides service discovery.

---

[**🚀 Next Topic: Storage**][obsidian://open?vault=Toyota&file=Personal%2FCKA%2F4%EF%B8%8F%E2%83%A3%20Storage%20(10%25)]
