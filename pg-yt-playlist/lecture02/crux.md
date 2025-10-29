## 🧭 Summary — *System Design for Beginners (Video 2)*

### 🎯 1. Goal of System Design

* System design = making an application **scalable** and **fault-tolerant**.
* Every company (Netflix, YouTube, Hotstar, etc.) has **different traffic patterns** and **use cases**, so their systems are designed differently.
* Balance between **reliability** (no crashes) and **cost efficiency**.

---

### ⚙️ 2. Scaling — Policies and Challenges

* **Scaling up** doesn’t happen magically; it follows defined **policies** like:

  * Requests/minute > threshold → add a server
  * CPU or Memory usage > 70% → spin up a new server
* **Gradual increase** in traffic = handled by auto-scaling.
* **Sudden spikes** (traffic bursts) can cause crashes before scaling happens.

---

### 🎬 3. Case Studies — How Different Companies Handle Scaling

#### 🟥 Netflix

* Predictable spikes (movie releases) → **pre-scaling** possible.
* Uses data to **warm up** extra servers before release.
* Can **cache initial content (e.g., first 10 mins)** globally using CDNs.
* If traffic doesn’t spike → scale down to save cost.

#### 🟥 YouTube

* Unpredictable spikes (viral videos, live streams).
* Must design for **unpredictable surges**.
* Auto-scaling is harder; needs very fast provisioning and global redundancy.

#### 🟥 Hotstar

* Predictable spikes (cricket matches) but **volatile during match hours**.
* May need to **turn off autoscaling** temporarily.
* Risk: scaling down non-critical services (like movies) may backfire when users switch mid-match.
* Uses **load/stress testing** before big events.

---

### 🧠 4. Evolution of Infrastructure

#### 🔹 Problem: Physical Machines

* Manual management: CPU, RAM, IPs, load balancer registration, etc.
* High overhead → less focus on application logic.

#### 🔹 Serverless (AWS Lambda)

* “Serverless” ≠ no servers — it means you **don’t manage** them.
* Upload code → AWS handles infrastructure.
* **Auto scales instantly**, pay-per-use.

  **Pros:**

  * Cheap
  * No management overhead

  **Cons:**

  * **Cold start latency** (first function call slow)
  * **Limited duration** per function
  * **No persistent state**
  * **DDOS can trigger many Lambdas → high cost**
  * **Vendor lock-in**
  * Need reverse proxy to handle **DB connection explosion**

---

### 💻 5. Virtualization → Containerization

#### 🧩 Virtual Machines (VMs)

* Fixes “It works on my local” issue.
* Each VM has OS + dependencies → heavy.
* **Still slow to spin up**, high resource usage.

#### 📦 Containers

* Lightweight “VMs” without OS layer.
* Share host OS → faster startup, less resource-heavy.
* Easier and faster scaling.

---

### 🤖 6. Container Orchestration

* Containers also need management:

  * Spinning up/down containers
  * Handling rolling updates
  * Scaling replicas
* This automation = **container orchestration**.

#### 🧱 From Borg → Kubernetes

* Google created **Borg** (internal).
* Then built **Kubernetes** (open-source) from those learnings.
* Kubernetes = brain that manages clusters of containers.
* Ensures **zero downtime** and efficient scaling.

---

### 🧪 7. Testing & Optimization

* Companies like Hotstar **simulate fake traffic** (load testing & stress testing) before peak events to ensure readiness.
* Continuous **monitoring + tuning** of system based on real traffic.

---

## 📘 Topics to Dig Deeper Into

### 🏗️ **System Design Fundamentals**

* Scalability vs. Fault Tolerance
* Load Balancing & Health Checks
* Auto-scaling policies (threshold-based, predictive, schedule-based)

### ☁️ **Cloud & Serverless**

* AWS Lambda, Azure Functions, Google Cloud Functions
* Cold start optimization
* Stateless architecture patterns
* Reverse proxy for DB connection pooling
* Vendor lock-in strategies

### 💾 **Virtualization & Containerization**

* Virtual Machines vs. Containers
* Docker basics (images, containers, layers)
* Container networking and volumes
* Differences between Hypervisor and Container Runtime

### ⚙️ **Container Orchestration**

* Kubernetes architecture (Pods, Nodes, ReplicaSets, Deployments, Services)
* Rolling updates, Blue-Green deployment
* Kubernetes scaling (HPA, Cluster Autoscaler)

### 📊 **Traffic Management & Caching**

* CDN basics
* Pre-scaling and warm-up strategies
* Caching policies (LRU, LFU, etc.)

### 🧪 **Testing & Observability**

* Load testing vs. Stress testing
* Monitoring tools (CloudWatch, Prometheus, Grafana)
* Log aggregation and alerting systems

### 🧩 **Design Case Studies**

* Netflix system design
* YouTube system design
* Hotstar/Disney+ Hotstar system design