# 🛡️ Linux Log Intrusion Detection  
### Using `/var/log/auth.log` and Simple Log Parsing

---

## 📌 Project Overview

This project demonstrates a simple method to detect failed SSH login attempts by analyzing the Linux authentication log:

/var/log/auth.log

yaml
Copy code

To generate test data, I created a small C++ program (`loop.cpp`) that triggers repeated failed SSH login attempts. Using tools like `grep`, `awk`, `sort`, and `uniq`, I extracted timestamps and IPs, created a CSV file, and generated a short intrusion summary report.

This project is beginner-friendly and helps understand how basic intrusion detection works in Linux.

---

## 🚀 Features

- Detect failed SSH login attempts  
- Extract timestamp and IP address  
- Normalize IPv6 loopback (`::1` → `127.0.0.1`)  
- Generate structured CSV: `failed_with_ts.csv`  
- Create summarised alert report: `alert_report.txt`  
- Automate failed log generation using C++ (`./loop`)

---

## 📂 Project Structure

├── loop.cpp # C++ script generating failed SSH attempts
├── failed_lines.txt # Extracted failed SSH log entries
├── failed_with_ts.csv # Processed CSV with timestamp + IP
├── alert_report.txt # Final intrusion summary report
├── screenshots/ # (Optional) Terminal screenshots
└── README.md

yaml
Copy code

---

## 🔧 Setup Instructions

### 1️⃣ Install required dependencies

```bash
sudo apt install -y rsyslog openssh-server sshpass
sudo systemctl enable --now rsyslog ssh
2️⃣ Verify that auth log exists
bash
Copy code
ls -l /var/log/auth.log
⚙️ C++ Test Log Generator
loop.cpp
This program creates multiple failed SSH login attempts for testing.

cpp
Copy code
#include <cstdlib>
#include <unistd.h>

int main() {
    for (int i = 1; i <= 15; ++i) {
        system("sshpass -p \"wrongpassword\" ssh "
               "-o StrictHostKeyChecking=no "
               "-o ConnectTimeout=2 "
               "-o BatchMode=no "
               "nonexistentuser@localhost exit");
        usleep(300000); // 0.3 seconds
    }
    return 0;
}
Compile and run:
bash
Copy code
g++ loop.cpp -o loop
./loop
📘 Step-by-Step Log Analysis
1️⃣ Extract failed SSH login attempts
bash
Copy code
sudo grep "Failed password" /var/log/auth.log > failed_lines.txt
2️⃣ Parse timestamp and IP using AWK
bash
Copy code
awk '{
  ip="";
  for(i=1;i<NF;i++){
    if($i=="from"){ ip=$(i+1); break }
  }
  if(ip){
    if(ip=="::1") ip="127.0.0.1";
    print $1","ip
  }
}' failed_lines.txt > failed_with_ts.csv
3️⃣ Generate the intrusion summary report
bash
Copy code
cut -d, -f2 failed_with_ts.csv | sort | uniq -c | sort -nr > alert_report.txt
📊 Example Output
alert_report.txt
Copy code
22 127.0.0.1
Meaning:
The local machine (127.0.0.1) made 22 failed SSH attempts → indicates brute-force behavior (intentionally generated for this project).

🧠 What I Learned
Understanding Linux authentication logs

Using grep and awk to extract data

Automating log generation with C++

Detecting brute-force patterns manually

Generating structured reports

This workflow is foundational for SOC analysts, cybersecurity learners, and Linux administrators.

📌 Next Steps
Add alert mechanism (email/webhook) for repeated failures

Add GeoIP lookup for external IP addresses

Build Python version of the parser

Visualize data in graphs

Integrate logs into ELK / Splunk / Wazuh

👤 Author
Saurabh Chikte
Student – Linux & Cybersecurity Enthusiast

If you want, I can also create:

📄 Resume project description
🎤 Interview explanation script
📦 GitHub description
📝 Short summary for LinkedIn

Just tell me “give resume line” or “interview script”.

Copy code

🚀





You said:
give in one go so that i can copy paste it it must be stylish good looking readme file for github repo

🚀

ChatGPT said:
Here is your final, stylish, polished, GitHub-ready README.md in ONE SINGLE BLOCK, perfectly formatted, visually attractive, and professional.

Just copy–paste and upload to your repo. ✅🔥

markdown
Copy code
<!-- Stylish README for GitHub -->

<h1 align="center">🛡️ Linux Log Intrusion Detection</h1>
<h3 align="center">Detecting Failed SSH Login Attempts Using <code>/var/log/auth.log</code></h3>

<p align="center">
  <img src="https://img.shields.io/badge/Linux-Log_Analysis-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/Category-Cybersecurity-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Language-C++-brightgreen?style=for-the-badge">
</p>

---

## 📌 Overview

This project demonstrates **how to detect failed SSH login attempts** by analyzing the Linux authentication log:

/var/log/auth.log

yaml
Copy code

A custom **C++ script (`loop.cpp`)** generates multiple failed SSH attempts for testing.  
Using standard Linux tools (`grep`, `awk`, `sort`, `uniq`), the log is processed to extract:

- Timestamps  
- IP addresses  
- Aggregated intrusion counts  

This project is perfect for **SOC Analyst beginners**, **Cybersecurity interns**, and **Linux learners**.

---

## 🚀 Features

✔ Extract failed SSH authentication events  
✔ Parse timestamps & IP addresses  
✔ Normalize IPv6 → IPv4 (`::1 → 127.0.0.1`)  
✔ Generate structured CSV file  
✔ Produce summary intrusion report  
✔ Local brute-force simulation using C++  

---

## 📂 Project Structure

├── loop.cpp # C++ generator for failed SSH attempts
├── failed_lines.txt # Extracted log lines
├── failed_with_ts.csv # Timestamp + IP CSV
├── alert_report.txt # Summary intrusion report
├── screenshots/ # Optional
└── README.md

yaml
Copy code

---

## 🔧 Setup Instructions

### 1️⃣ Install dependencies

```bash
sudo apt install -y rsyslog openssh-server sshpass
sudo systemctl enable --now rsyslog ssh
2️⃣ Confirm that auth log exists
bash
Copy code
ls -l /var/log/auth.log
⚙️ C++ Log Generator
A small C++ script used to intentionally create failed SSH login attempts:

cpp
Copy code
#include <cstdlib>
#include <unistd.h>

int main() {
    for (int i = 1; i <= 15; ++i) {
        system("sshpass -p \"wrongpassword\" ssh "
               "-o StrictHostKeyChecking=no "
               "-o ConnectTimeout=2 "
               "-o BatchMode=no "
               "nonexistentuser@localhost exit");
        usleep(300000); // 0.3 seconds
    }
    return 0;
}
Compile & Run
bash
Copy code
g++ loop.cpp -o loop
./loop
📝 Step-by-Step Log Analysis
1️⃣ Extract failed SSH login entries
bash
Copy code
sudo grep "Failed password" /var/log/auth.log > failed_lines.txt
2️⃣ Parse timestamp + IP into CSV
bash
Copy code
awk '{
  ip="";
  for(i=1;i<NF;i++){
    if($i=="from"){ ip=$(i+1); break }
  }
  if(ip){
    if(ip=="::1") ip="127.0.0.1";
    print $1","ip
  }
}' failed_lines.txt > failed_with_ts.csv
3️⃣ Generate intrusion report
bash
Copy code
cut -d, -f2 failed_with_ts.csv | sort | uniq -c | sort -nr > alert_report.txt
📊 Example Output
📄 alert_report.txt
Copy code
22 127.0.0.1
Meaning:
The local machine performed 22 failed SSH attempts (generated by ./loop).
This demonstrates basic brute-force detection.

🧠 Learnings & Concepts Covered
Understanding Linux authentication logs

SSH authentication failure patterns

Log parsing using grep, awk

Creating structured datasets (CSV)

Detecting brute-force patterns manually

Using C++ to simulate attacks

📌 Future Enhancements
🔹 Add alerting (email/webhook)
🔹 Integrate GeoIP lookup
🔹 Create Python-based parser
🔹 Visualize results using Grafana/Matplotlib
🔹 Integrate with ELK / Splunk / Wazuh

👤 Author
Saurabh Chikte
Cybersecurity & Linux Enthusiast

📧 Contact available on request
🔗 Portfolio link can be added here
