# 🔐 Secure and Monitored Web Infrastructure (www.foobar.com)

## 📌 Overview

A robust infrastructure to host `www.foobar.com` with:
- Encrypted HTTPS traffic
- Proper network segmentation with firewalls
- Monitoring agents collecting metrics
- Load balancing and database replication

---

## 🧱 Components

### 🔒 Firewalls (3 Total)
- **Firewall 1**: Between internet and load balancer (network perimeter)
- **Firewall 2**: Between load balancer and application servers
- **Firewall 3**: Between app servers and databases

✅ **Why?** To isolate components, reduce attack surfaces, and enforce security policies.

---

### 🔐 HTTPS with SSL Certificate
- **Served at the Load Balancer (HAProxy)**
- Terminating SSL here simplifies server config, but comes with trade-offs.

✅ **Why?** Encrypts traffic, protects user data, and establishes trust.

⚠️ **Issue**: If SSL is terminated at the load balancer, internal traffic is unencrypted unless re-encrypted — exposing sensitive data if the internal network is compromised.

---

### 📊 Monitoring Clients
- Installed on each server (e.g., **Sumologic**, **Datadog**, **Prometheus agent**)
- Collect metrics: CPU, memory, disk, request rate, etc.

✅ **Why?** Enables observability, diagnostics, and alerting.

**To monitor web server QPS (Queries Per Second):**
- Use Nginx metrics or logs + monitoring agent
- Send QPS data to centralized dashboard
- Set alert thresholds to detect anomalies

---

## ⚙️ Infrastructure

### 🔄 Load Balancer (HAProxy)
- Handles incoming HTTPS requests
- Distributes load using **Round-Robin**
- SSL termination occurs here

✅ **Active-Active setup** for high availability

---

### 🖥️ Servers (x3)
Each contains:
- **Web server** (Nginx)
- **App server** (PHP)
- **Application code**
- **Database** (MySQL)
  - **S1** = Primary (write-enabled)
  - **S2 & S3** = Replicas (read-only)

✅ **Database Replication**:
- Primary handles writes
- Replicas sync data and handle reads

⚠️ **Issue**: Only one node can handle writes → limits scalability and fault tolerance

⚠️ **Identical Components Problem**:
- Combining app and DB on same machine creates noisy neighbors
- Harder to scale specific layers (e.g., DB vs App)

---

## ❗ Known Issues

| Issue | Description |
|-------|-------------|
| **SSL Termination at LB** | Unencrypted internal traffic if not re-encrypted |
| **MySQL Write Limitation** | Only one primary node = bottleneck and risk |
| **Monolithic Servers** | All services on each server = resource contention |
| **No Auto-Scaling** | No elasticity to handle large spikes |
| **Manual Failover** | If primary DB fails, requires promotion of replica manually |

---

## ✅ Improvements to Consider

- Enable SSL passthrough or re-encrypt after LB
- Add failover-capable MySQL clusters (Galera, MySQL Group Replication)
- Separate app, web, and DB layers
- Add alerting + dashboards (Grafana, Sumologic)
- Add HTTPS at the app level for E2E encryption

