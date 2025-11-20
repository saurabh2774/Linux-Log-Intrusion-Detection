# Linux-Log-Intrusion-Detection
Analyzed Linux authentication logs (/var/log/auth.log) to identify failed SSH login attempts, brute-force behavior, and suspicious login patterns. Used grep and awk to extract login failures, summarize attacker IPs, and generate a basic alert report. Gained hands-on experience in log analysis, threat detection, and incident documentation.
# 🔐 Linux Log Intrusion Detection

This project focuses on analyzing Linux authentication logs (`/var/log/auth.log`) to detect suspicious SSH login attempts, brute-force activity, and unusual login patterns. It is a beginner-friendly SOC (Security Operations Center) style project designed to build hands-on cybersecurity skills such as log analysis, threat detection, and basic incident investigation.

---

## 📌 Project Overview

Linux systems record all authentication events inside the `auth.log` file.  
In this project, we:

- Detect **failed SSH login attempts**
- Identify **brute-force attack patterns**
- Extract and summarize **attacker IP addresses**
- Count **number of failed attempts**
- Observe login timestamps for suspicious behavior
- Generate a beginner-friendly **incident summary report**

This project simulates real SOC Tier-1 analyst tasks.

---

## 🛠️ Tools & Technologies Used

- **Linux (Ubuntu/Debian)**  
- **Terminal / Bash**  
- **grep, awk, wc, sort, uniq**  
- **SSH Authentication Logs**  
- **Basic Shell Scripting**  
- **Incident Documentation**

  
---

## ▶️ How to Run the Script

1. Clone the repo:
```bash
git clone <your-repository-url>
cd linux-log-intrusion-detection
# Show all failed login attempts
grep "Failed password" /var/log/auth.log

# Count total failed attempts
grep "Failed password" /var/log/auth.log | wc -l

# List attacker IPs and sort them by frequency
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
Total Failed Attempts: 15

Top Attacker IPs:
     10 192.168.1.10
      5 45.23.10.8


---

## 📂 Repository Structure

