# Systems & Network Engineering Assessment

This repository contains technical solutions for automation and monitoring tasks, specifically focusing on high-traffic environments and SSL offloading.

## Task 1: Random Number Generator

### Description
A Bash script that produces numbers 1-10 in a random, non-repeating order. Each execution ensures that every number in the range appears exactly once.

### Usage Instructions
1. Grant execution permissions to the script:
   `chmod +x random_gen.sh`
2. Run the script:
   `./random_gen.sh`

### Verification (Tests)
To verify the script's integrity, run the following commands:
- **Uniqueness Test:** `./random_gen.sh | sort -u | wc -l` (Expected result: 10)
- **Range Test:** `./random_gen.sh | awk '$1 < 1 || $1 > 10 {exit 1}' && echo "Pass" || echo "Fail"` (Expected result: Pass)

---

## Task 2: Monitoring Strategy

### Overview
A comprehensive analysis of monitoring a high-load SSL proxy server handling 25,000 requests per second (RPS).

### Implementation Details
The full strategy, including key metrics (PPS, SSL Latency, Softirqs) and technical challenges (Observer Effect, Disk I/O), is documented in the separate file: [monitoring_strategy.md](./monitoring_strategy.md).

---
*Note: This project is part of a technical assessment.*
