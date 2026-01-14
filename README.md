# Cloud Security and Multi-Cloud Student Portal

![AWS](https://img.shields.io/badge/AWS-EC2%20%7C%20S3-orange)
![Azure](https://img.shields.io/badge/Azure-Virtual%20Machines-blue)
![Splunk](https://img.shields.io/badge/Splunk-SOAR%20%7C%20Enterprise-green)
![WordPress](https://img.shields.io/badge/WordPress-LearnPress-blueviolet)

## 📖 Project Overview
This project delivers a secure, distributed **WordPress-based student portal** hosted in a hybrid cloud environment. It integrates **AWS EC2** for web hosting, **Azure Virtual Machines** for MySQL database management, and **AWS S3** for scalable media storage. 

The core research focuses on enhancing distributed systems security by combining cloud-native logging (**AWS CloudTrail**, **Azure Log Analytics**) with **Splunk SOAR** to automate threat detection and incident response.

### Key Features
- **Hybrid Cloud Architecture:** Leverages AWS compute and Azure database services[cite: 35].
- **Automated Security:** Implements Splunk SOAR playbooks to detect and respond to unauthorized access (e.g., failed logins).
- **Centralized Logging:** Aggregates logs from multiple clouds into a single dashboard with >95% event capture accuracy.
- **Scalable Storage:** Offloads media to AWS S3 using the WP Offload Media plugin.

---

## 🏗️ System Architecture

| Component | Service | Description |
| :--- | :--- | :--- |
| **Web Server** | AWS EC2 (t2.micro) | [cite_start]Hosts WordPress (Ubuntu 20.04), Apache, PHP, and LearnPress. |
| **Database** | Azure VM (B1s) | [cite_start]Hosts MySQL Server (Ubuntu 22.04), secured via WireGuard. |
| **Storage** | AWS S3 | [cite_start]Stores static assets and media uploads (`student-portal-content`). |
| **Logging** | CloudTrail & Azure Monitor | [cite_start]Captures API activity and Database logs. |
| **Orchestration** | Splunk SOAR | [cite_start]Automates incident response workflows. |

---

## 🚀 Installation & Deployment

### Prerequisites
- AWS Account (EC2, S3, IAM roles)
- Azure Account (Virtual Machines, Log Analytics)
- Splunk Enterprise & SOAR (Community Edition)

### Step 1: Web Portal (AWS)
1. Launch an **EC2 t2.micro** instance.
2. Install **Apache**, **PHP**, and **WordPress**.
3. [cite_start]Install the **LearnPress** plugin for course management.

### Step 2: Database (Azure)
1. Provision an **Azure VM** (Ubuntu 22.04).
2. Install **MySQL Server** and configure tables for WordPress[cite: 122].
3. Set up **WireGuard** to secure the connection between AWS EC2 and Azure VM.

### Step 3: Storage Integration
1. Create an S3 bucket: `student-portal-content`.
2. Configure **IAM roles** for secure access.
3. [cite_start]Install **WP Offload Media Lite** on WordPress to sync media to S3.

### Step 4: Logging & SOAR Setup
1. [cite_start]**AWS:** Enable **CloudTrail** to log events to a dedicated S3 bucket (`student-portal-logs`).
2. [cite_start]**Azure:** Install **Azure Monitor Agent (AMA)** to ingest `/var/log/mysql/mysql.log`.
3. **Splunk:** Deploy Splunk on an AWS EC2 `t2.large` instance.
4. [cite_start]**Automation:** Deploy the `WordPress_Login_Alert` playbook in Splunk SOAR to trigger alerts on failed logins.

---

## 📊 Results & Validation

The system was validated with **100 MySQL queries** and **50 simulated login attempts** (25 failed).

| Metric | Goal | Achieved Result |
| :--- | :--- | :--- |
| **Log Capture Rate** | >95% | [cite_start]**95%+** (100% CloudTrail, 95% Azure)  |
| **Threat Detection** | >90% | [cite_start]**90%** (45/50 attacks detected) |
| **Response Time** | Reduce by 50% | [cite_start]**10 seconds** (vs 20s manual)  |
| **Uptime** | High Availability | [cite_start]**99.9%** (over 7 days) |

