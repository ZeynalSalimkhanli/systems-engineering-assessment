# Task 2: Monitoring Strategy for High-Traffic SSL Proxy

## System Analysis
- **Hardware:** 4x Intel Xeon E7-4830 v4, 64GB RAM, 2x10Gbit/s NICs.
- **Workload:** SSL Offloading at 25,000 Requests Per Second (RPS).

## 1. Key Metrics to Monitor
* **Network PPS (Packets Per Second):** At 25k RPS, monitoring PPS is more critical than just bandwidth. High PPS can saturate the CPU's interrupt handling before the 10Gbps link is full.
* **SSL/TLS Handshake Latency:** This measures the efficiency of the SSL offloading. Any spike indicates that the Xeon CPUs are struggling with cryptographic operations.
* **CPU Softirqs:** Crucial for high-traffic servers. It shows how much time CPUs spend handling network packets. We must ensure load is balanced across all 4 CPUs.
* **TCP Connection States:** Monitoring `ESTABLISHED` and `TIME_WAIT` counts to prevent ephemeral port exhaustion, which is common at 25k RPS.
* **Disk I/O Wait:** Since the server has HDDs, logging 25k requests/sec can cause I/O bottlenecks. Monitoring 'iowait' is essential.

## 2. Methodology & Tools
* **Prometheus + Node Exporter:** For collecting hardware and OS-level metrics.
* **Nginx/HAProxy Exporter:** To gather application-specific metrics like active connections and error rates (4xx/5xx).
* **Grafana:** For real-time visualization and setting up critical alerts.

## 3. Monitoring Challenges
* **The Observer Effect:** The monitoring agent itself must be extremely lightweight; otherwise, the act of monitoring could crash a server already under 25k RPS load.
* **Log Bursting:** Writing logs for 25,000 events/sec will quickly exhaust the 2TB HDD. Log rotation and sampling strategies are required.
* **Data Granularity:** Standard 1-minute scraping might miss micro-bursts that cause temporary service outages.
