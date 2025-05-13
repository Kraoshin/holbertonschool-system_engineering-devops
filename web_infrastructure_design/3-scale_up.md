# ⚙️ Split Web Infrastructure with Load Balancer Cluster

This design outlines a scalable and modular web infrastructure hosting a website such as **www.foobar.com**, featuring **split service components** and **redundant load balancers configured as a cluster**.

---

## 🧱 Infrastructure Components

### 1. 🖥️ Server Roles

Instead of combining all roles on a single server, we split services across dedicated servers to improve performance, maintainability, and scalability:

#### 🟦 Web Server
- **Technology**: Nginx or Apache
- **Role**: Handles incoming HTTP/HTTPS requests and serves static content.
- **Why?**
  - Isolates web-specific concerns
  - Allows independent scaling of the web layer

#### 🟨 Application Server
- **Technology**: PHP-FPM, Node.js, Python, etc.
- **Role**: Executes application logic (e.g., rendering pages, managing sessions).
- **Why?**
  - Improves maintainability by separating logic from presentation
  - Easier debugging and tuning

#### 🟩 Database Server
- **Technology**: MySQL, PostgreSQL
- **Role**: Stores and manages persistent application data
- **Why?**
  - Enhances security by isolating access
  - Supports better performance tuning for database queries

---

### 2. 🔁 Load Balancer Cluster (HAProxy)

- **Technology**: HAProxy
- **Setup**: Two HAProxy nodes configured in an **active-passive cluster**
- **Role**: Distributes traffic to the web server(s) and acts as the entry point for the system.

#### ✅ Why add a load balancer cluster?
- **High availability**: If one load balancer fails, the second takes over (failover).
- **Scalability**: Easily add more backend servers behind the load balancer.
- **Centralized control**: Routes traffic intelligently (e.g., round-robin, least connections).

---

## 🛠️ Architectural Benefits

| Component          | Purpose                                                                 |
|-------------------|-------------------------------------------------------------------------|
| Web Server         | Efficiently serves static content (HTML, CSS, JS)                      |
| Application Server | Separates application logic for maintainability and security           |
| Database Server    | Dedicated data storage and transaction management                      |
| Load Balancer (LB) | Distributes traffic and ensures uptime through clustering              |

---

## 🔍 Summary

This infrastructure improves:

- **Security** (isolated DB)
- **Maintainability** (split roles)
- **Resilience** (LB cluster)
- **Scalability** (each layer can be scaled independently)

By splitting components and using a redundant load balancing setup, we prepare the infrastructure for growth and fault tolerance, making it production-ready.
