# Systems & Network Engineering Assessment

This repository contains solutions for automation and monitoring tasks, focusing on high-performance systems and real-world production scenarios.

---

## Task 1: Random Number Generator

### Description
A Bash script that generates numbers from 1 to 10 in a random order without repetition. Each execution ensures all numbers appear exactly once.

---

### Build Instructions
```bash
chmod +x random_gen.sh
```

---

### Usage
```bash
./random_gen.sh
```

---

### Verification (Tests)

#### Line Count Test
```bash
./random_gen.sh | wc -l
# Expected output: 10
```

#### Uniqueness Test
```bash
./random_gen.sh | sort -u | wc -l
# Expected output: 10
```

#### Range Test
```bash
./random_gen.sh | awk '$1 < 1 || $1 > 10 {exit 1}' && echo "Pass" || echo "Fail"
# Expected output: Pass
```

---

### Known Limitations
- Requires `shuf` (GNU coreutils)
- May not work on minimal systems where `shuf` is not available

---

## Task 2: Monitoring Strategy

### Overview
A monitoring design for a high-load SSL proxy server handling approximately 25,000 requests per second (RPS).

---

### Details
The full monitoring strategy, including:
- Key system and application metrics
- Monitoring tools and architecture
- Alerting strategy
- Real-world challenges

is documented here:

👉 **monitoring_strategy.md**

---

## Project Notes
- Focused on real-world production scenarios
- Designed with scalability and performance in mind
- Includes validation tests and structured documentation
