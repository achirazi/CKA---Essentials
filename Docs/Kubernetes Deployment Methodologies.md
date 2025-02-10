
## **1️⃣ Rolling Updates**
- **Overview**:
  - Incrementally replaces old pods with new ones.
  - Ensures zero downtime during deployment.
- **How It Works**:
  - New pods are created before old ones are terminated.
  - Can configure maxUnavailable and maxSurge.
- **Example YAML**:
  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: rolling-update-deployment
  spec:
    replicas: 3
    strategy:
      type: RollingUpdate
      rollingUpdate:
        maxUnavailable: 1
        maxSurge: 1
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
- **Commands**:
  ```sh
  kubectl rollout status deployment rolling-update-deployment
  kubectl rollout undo deployment rolling-update-deployment
  ```

---

## **2️⃣ Recreate Strategy**
- **Overview**:
  - Deletes all old pods before creating new ones.
  - Causes downtime during deployment.
- **Use Cases**:
  - Suitable for applications that **don’t require high availability**.
  - Useful for major database schema changes.
- **Example YAML**:
  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: recreate-deployment
  spec:
    strategy:
      type: Recreate
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
- **Commands**:
  ```sh
  kubectl rollout status deployment recreate-deployment
  ```

---

## **3️⃣ Blue-Green Deployment**
- **Overview**:
  - Two environments (**Blue** = old, **Green** = new).
  - Switch traffic to new environment after validation.
- **How It Works**:
  - Deploy the new version (Green) alongside the old (Blue).
  - Traffic is switched once the new version is stable.
  - The old version (Blue) remains for rollback.
- **Example Setup with Services**:
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: my-app
  spec:
    selector:
      app: blue
    ports:
      - protocol: TCP
        port: 80
        targetPort: 8080
  ```
  - To switch to **Green**, update the selector to `app: green`.
- **Commands**:
  ```sh
  kubectl get services
  kubectl edit service my-app
  ```

---

## **4️⃣ Canary Deployment**
- **Overview**:
  - Gradually releases new versions to a small subset of users.
  - If stable, gradually increase rollout percentage.
- **Use Cases**:
  - Used for **testing in production** before full release.
- **Example Canary Deployment**:
  ```yaml
  apiVersion: apps/v1
  kind: Deployment
  metadata:
    name: canary-deployment
  spec:
    replicas: 1
    selector:
      matchLabels:
        app: my-app
        version: canary
    template:
      metadata:
        labels:
          app: my-app
          version: canary
      spec:
        containers:
        - name: nginx
          image: nginx:latest
  ```
- **Commands**:
  ```sh
  kubectl get deployments
  ```

---

## **5️⃣ A/B Testing Deployment**
- **Overview**:
  - Routes different versions based on conditions (e.g., region, device type).
  - Requires **Ingress Controller or Service Mesh (Istio, Linkerd).**
- **Example A/B Testing with Istio**:
  ```yaml
  apiVersion: networking.istio.io/v1alpha3
  kind: VirtualService
  metadata:
    name: my-app
  spec:
    hosts:
    - my-app.example.com
    http:
    - match:
      - headers:
          user-agent:
            regex: ".*(iPhone|iPad).*"
      route:
      - destination:
          host: my-app
          subset: version-v2
    - route:
      - destination:
          host: my-app
          subset: version-v1
  ```
- **Commands**:
  ```sh
  kubectl get virtualservice
  ```

---