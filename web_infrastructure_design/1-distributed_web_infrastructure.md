# 🌐 Three-Server Web Infrastructure (www.foobar.com)

## 📊 Diagram

Diagram: `three_server_web_infrastructure.png`  
(*Generated using Graphviz – shows the relationship between user, DNS, load balancer, and backend servers.*)

---

## ✅ Components Breakdown

### 1. **Load Balancer (HAProxy)**
- **Why?** Distributes incoming web traffic across multiple servers to improve availability and scalability.
- **IP Address:** 8.8.8.8
- **Distribution Algorithm:** Round-Robin
  - **How it works:** Each incoming request is sent to the next server in line (S1, then S2, then back to S1, etc.).
- **Setup:** Active-Active
  - **Active-Active:** Both Server 1 and Server 2 serve traffic simultaneously.
  - **Active-Passive (by contrast):** Only one server serves traffic while the other is on standby.

### 2. **Servers (x2)**
Each server contains:
- **Web Server:** Nginx – handles HTTP requests.
- **Application Server:** PHP-FPM – processes PHP logic.
- **Codebase:** The actual application code.
- **Database:**
  - Server 1 hosts the **Primary MySQL** instance.
  - Server 2 hosts the **Replica MySQL** instance.

---

## 🔄 Database Setup

### Primary-Replica (Master-Slave) Configuration

- **Primary Node (Server 1)**:
  - Handles all **write** operations (INSERT, UPDATE, DELETE).
- **Replica Node (Server 2)**:
  - Handles **read-only** queries (SELECT) to reduce load on the primary.
- Replication is **asynchronous**, meaning there's a slight delay in data consistency between primary and replica.

---

## ❗ Issues with This Infrastructure

### 1. **Single Point of Failure (SPOF)**
- The **Load Balancer** is a SPOF. If it fails, the entire site becomes unreachable.

### 2. **Security**
- No **firewall** to control or filter malicious access.
- No **HTTPS**, so data in transit is not encrypted (risk of man-in-the-middle attacks).

### 3. **Monitoring**
- No monitoring system in place (e.g., for server health, uptime, traffic load).
- No alerting mechanism for failures or performance issues.

---

## ✅ Summary

| Component       | Purpose                                      |
|----------------|----------------------------------------------|
| Load Balancer   | Distributes traffic across multiple servers |
| Nginx           | Handles HTTP/S traffic                      |
| PHP-FPM         | Executes server-side logic                  |
| MySQL Primary   | Main database for writes                    |
| MySQL Replica   | Read-only replica for load balancing reads  |
