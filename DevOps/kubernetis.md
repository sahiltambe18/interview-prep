---

# **1. What is Kubernetes, and Why Do We Use It?**
### **What is Kubernetes?**
**Kubernetes (K8s)** is an **open-source container orchestration platform** that automates the deployment, scaling, and management of containerized applications. It was originally developed by **Google** and is now maintained by the **Cloud Native Computing Foundation (CNCF).**

### **Why Use Kubernetes?**
✅ **Automated Scaling** – Dynamically scale applications based on demand.  
✅ **Load Balancing** – Distribute traffic efficiently across containers.  
✅ **Self-Healing** – Restarts failed containers automatically.  
✅ **Rolling Updates & Rollbacks** – Deploy new versions **without downtime**.  
✅ **Declarative Configuration** – Manage infrastructure using YAML files.  
✅ **Multi-Cloud Support** – Works on AWS, GCP, Azure, or on-premises.  

---
# **2. How Do You Scale Applications Using Kubernetes?**
Scaling in Kubernetes can be done **manually or automatically** using:

### **1️⃣ Manual Scaling with `kubectl`**
You can **increase or decrease** the number of running Pods manually.
```bash
kubectl scale deployment my-app --replicas=5
```
This increases `my-app` to **5 instances**.

### **2️⃣ Horizontal Pod Autoscaler (HPA) – Auto Scaling**
HPA **automatically scales Pods** based on **CPU, memory, or custom metrics**.
#### **Example: HPA for CPU-Based Scaling**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: my-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: my-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 50
```
👉 Kubernetes will automatically **increase or decrease** replicas based on CPU usage.

### **3️⃣ Vertical Pod Autoscaler (VPA) – Adjust Resource Requests**
VPA automatically **adjusts the CPU and memory requests** of a Pod instead of scaling replicas.

### **4️⃣ Cluster Autoscaler – Scale Worker Nodes**
Cluster Autoscaler adds or removes **worker nodes** in cloud environments like AWS, GCP, or Azure when needed.

---
# **3. What Is the Role of Deployments, Services, and Ingress in Kubernetes?**
Kubernetes uses **Deployments, Services, and Ingress** to manage applications.

## **1️⃣ Deployments (Managing Pods)**
A **Deployment** is a Kubernetes resource that manages a set of identical **Pods**.
- Ensures **desired state** is maintained.
- Supports **rolling updates and rollbacks**.

#### **Example: Deployment for a Node.js App**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
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
        - name: my-app
          image: my-app-image:latest
          ports:
            - containerPort: 3000
```
👉 This ensures that **3 instances** of `my-app` are always running.

---

## **2️⃣ Services (Exposing Pods)**
A **Service** is used to expose a set of Pods to **other services or the internet**.

**Types of Services:**
| Service Type  | Use Case |
|--------------|-------------|
| **ClusterIP** (default) | Internal communication between Pods. |
| **NodePort** | Exposes the service on a static port on each Node. |
| **LoadBalancer** | Exposes the service to the internet (for cloud providers). |
| **ExternalName** | Maps to an external DNS name. |

#### **Example: ClusterIP Service for Internal Communication**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
```
👉 This service allows other Pods to access `my-app` on port **80**.

---

## **3️⃣ Ingress (Routing External Traffic)**
Ingress is used to **route external traffic** to Kubernetes Services using a domain name.

#### **Example: Ingress for Routing Traffic to `my-app`**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
spec:
  rules:
    - host: myapp.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: my-app-service
                port:
                  number: 80
```
👉 This directs requests from **myapp.example.com** to `my-app-service`.

---

# **4. How Do You Manage Secrets in Kubernetes?**
Kubernetes **Secrets** store **sensitive information** like passwords, API keys, and tokens.

## **1️⃣ Creating a Secret Manually**
```bash
kubectl create secret generic my-secret --from-literal=DB_PASSWORD=supersecret
```
👉 This creates a secret named `my-secret`.

## **2️⃣ Using Secrets in a Pod**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
spec:
  containers:
    - name: my-app
      image: my-app-image
      env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: my-secret
              key: DB_PASSWORD
```
👉 The Pod retrieves the secret and sets it as an **environment variable**.

---

# **5. What’s the Difference Between StatefulSets and Deployments?**
| Feature  | **StatefulSet** | **Deployment** |
|----------|---------------|-------------|
| Use Case | **Stateful apps** (DBs, Kafka, Redis) | **Stateless apps** (APIs, Web Apps) |
| Pod Naming | Each Pod has a unique, persistent name (e.g., `my-app-0`, `my-app-1`). | Pods are created randomly (e.g., `my-app-xyz`). |
| Storage | Uses **Persistent Volume Claims (PVCs)** that stick with Pods. | Pods are recreated with fresh storage. |
| Ordering | Pods start **in order** and shut down **in order**. | Pods start and stop randomly. |

#### **Example: StatefulSet for a Database**
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: my-db
spec:
  serviceName: "my-db-service"
  replicas: 3
  selector:
    matchLabels:
      app: my-db
  template:
    metadata:
      labels:
        app: my-db
    spec:
      containers:
        - name: my-db
          image: postgres:latest
          volumeMounts:
            - name: db-storage
              mountPath: /var/lib/postgresql/data
  volumeClaimTemplates:
    - metadata:
        name: db-storage
      spec:
        accessModes: ["ReadWriteOnce"]
        resources:
          requests:
            storage: 10Gi
```
👉 Each DB Pod will have its **own storage**, even if it restarts.

---
