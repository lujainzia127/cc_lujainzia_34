# Project 9 - Infrastructure Monitoring and Log Collection System

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                   👥 Administrators / DevOps Team                │
│              Manage Infrastructure | Deploy | Monitor            │
└───────────────────────────────┬─────────────────────────────────┘
                                │
                                │ Git Push / Terraform Apply / Ansible
                                ▼
                ┌───────────────────────────────────────┐
                │      📦 Git Repository (GitHub)       │
                │                                       │
                │  • Terraform Infrastructure Code      │
                │  • Ansible Playbooks & Roles          │
                │  • Bash Monitoring Scripts            │
                │  • Dashboard Templates (HTML/CSS)     │
                │  • Configuration Files                │
                └───────────────┬───────────────────────┘
                                │
                                │ terraform apply / ansible-playbook
                                ▼
┌───────────────────────────────────────────────────────────────────────┐
│                        ☁️  AWS VPC (10.0.0.0/16)                      │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │           🌐 Public Subnet (10.0.1.0/24)                        │ │
│  │                                                                 │ │
│  │   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓                │ │
│  │   ┃    🖥️  Monitoring Server (EC2)           ┃                │ │
│  │   ┃                                           ┃                │ │
│  │   ┃  📊 Web Dashboard (Nginx):               ┃                │ │
│  │   ┃    • Serves static HTML dashboard        ┃                │ │
│  │   ┃    • Shows server status (UP/DOWN)       ┃                │ │
│  │   ┃    • Displays metrics & reports          ┃                │ │
│  │   ┃    • Accessible: HTTP (Port 80)          ┃                │ │
│  │   ┃                                           ┃                │ │
│  │   ┃  🔧 Monitoring Scripts:                  ┃                │ │
│  │   ┃    • collect-metrics.sh                  ┃                │ │
│  │   ┃      (CPU, Memory, Disk usage)           ┃                │ │
│  │   ┃    • check-services.sh                   ┃                │ │
│  │   ┃      (systemctl status checks)           ┃                │ │
│  │   ┃    • http-health-check.sh                ┃                │ │
│  │   ┃      (curl /health endpoints)            ┃                │ │
│  │   ┃    • build-dashboard.sh                  ┃                │ │
│  │   ┃      (updates HTML dashboard)            ┃                │ │
│  │   ┃    • generate-report.sh                  ┃                │ │
│  │   ┃      (daily/weekly reports)              ┃                │ │
│  │   ┃                                           ┃                │ │
│  │   ┃  ⏰ Automation (Cron Jobs):              ┃                │ │
│  │   ┃    • Every 5 min: Health checks          ┃                │ │
│  │   ┃    • Daily: Generate daily report        ┃                │ │
│  │   ┃    • Weekly: Generate weekly report      ┃                │ │
│  │   ┃                                           ┃                │ │
│  │   ┃  📁 Storage:                             ┃                │ │
│  │   ┃    • /var/www/html/logs/ (collected)     ┃                │ │
│  │   ┃    • /var/www/html/reports/ (generated)  ┃                │ │
│  │   ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛                │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                                                                       │
│                    │                                                  │
│                    │ SSH + HTTP Health Checks + Ansible Fetch         │
│                    │                                                  │
│                    ▼                                                  │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │           🔒 Private Subnet (10.0.2.0/24)                       │ │
│  │                                                                 │ │
│  │   ┌──────────────────┐      ┌──────────────────┐               │ │
│  │   │ 🚀 App Server 1  │      │ 🚀 App Server 2  │               │ │
│  │   │                  │      │                  │               │ │
│  │   │ • Nginx          │      │ • Nginx          │               │ │
│  │   │ • /health (200)  │      │ • /health (200)  │               │ │
│  │   │ • access.log     │      │ • access.log     │               │ │
│  │   │ • error.log      │      │ • error.log      │               │ │
│  │   └──────────────────┘      └──────────────────┘               │ │
│  │                                                                 │ │
│  │   ┌──────────────────┐      ┌──────────────────┐               │ │
│  │   │ 🚀 App Server 3  │      │ 🚀 App Server N  │               │ │
│  │   │                  │      │                  │               │ │
│  │   │ • Nginx          │      │ • Nginx          │               │ │
│  │   │ • /health (200)  │      │ • /health (200)  │               │ │
│  │   │ • access.log     │      │ • access.log     │               │ │
│  │   │ • error.log      │      │ • error.log      │               │ │
│  │   └──────────────────┘      └──────────────────┘               │ │
│  └─────────────────────────────────────────────────────────────────┘ │
│                                                                       │
│  ┌─────────────────────────────────────────────────────────────────┐ │
│  │ 🌐 Internet Gateway | 🛡️ Security Groups | 🔐 SSH Key Auth      │ │
│  └─────────────────────────────────────────────────────────────────┘ │
└───────────────────────────────────────────────────────────────────────┘
```

## 🔄 System Data Flow

**1. Infrastructure Provisioning (Terraform):**
   - Creates VPC with CIDR 10.0.0.0/16
   - Creates public subnet (10.0.1.0/24) for monitoring server
   - Creates private subnet (10.0.2.0/24) for app servers
   - Provisions Internet Gateway and Route Tables
   - Creates Security Groups (Monitoring SG, App SG)
   - Launches EC2 instances (1 monitoring + N app servers)

**2. Server Configuration (Ansible):**
   - **App Servers:**
     - Installs Nginx web server
     - Configures /health endpoint (returns HTTP 200)
     - Sets up access and error logging
   - **Monitoring Server:**
     - Installs Nginx to serve dashboard
     - Deploys all monitoring scripts to /usr/local/bin/
     - Configures cron jobs for automated monitoring
     - Sets up log and report directories

**3. Health Monitoring (Every 5 minutes via Cron):**
   - `collect-metrics.sh` → Gathers CPU, memory, disk usage from all servers
   - `check-services.sh` → Verifies Nginx service status (systemctl)
   - `http-health-check.sh` → Tests /health endpoint on each app server
   - `build-dashboard.sh` → Updates static HTML dashboard with latest status

**4. Log Collection (Ansible Playbook):**
   - Runs periodically using `collect-logs.yml` playbook
   - Uses `ansible.builtin.fetch` module to retrieve logs
   - Collects `/var/log/nginx/access.log` and `/var/log/nginx/error.log`
   - Stores on monitoring server: `/var/www/html/logs/{hostname}/{date}/`
   - Organizes by hostname and timestamp

**5. Report Generation (Cron):**
   - **Daily Report:** `generate-report.sh daily`
     - Saved to: `/var/www/html/reports/daily-YYYY-MM-DD.txt`
     - Contains: server status, uptime, health check results, resource usage
   - **Weekly Report:** `generate-report.sh weekly`
     - Saved to: `/var/www/html/reports/weekly-YYYY-WW.txt`
     - Contains: weekly summary, trends, incidents, log analysis

**6. Dashboard Access:**
   - Administrators access via: `http://<monitoring-server-public-ip>`
   - Dashboard displays:
     - Real-time server status (UP/DOWN indicators)
     - Latest metrics (CPU, memory, disk usage)
     - Links to collected logs
     - Links to daily/weekly reports
     - Historical data visualization

## 🛡️ Network Security

| Component | Access Rule | Description |
|-----------|-------------|-------------|
| **Internet Gateway** | Public access | Routes traffic from internet to public subnet |
| **Monitoring Server SG** | HTTP (80) from anywhere<br>SSH (22) from admin IPs | Dashboard accessible via browser<br>Secure admin access |
| **App Server SG** | HTTP (80) from Monitoring SG only<br>SSH (22) from admin IPs | Only monitoring server can check health<br>Secure admin access |
| **SSH Keys** | Key-based authentication | No password authentication allowed |

## 📊 Monitoring Metrics Collected

| Metric | Command/Script | Frequency |
|--------|----------------|-----------|
| **CPU Usage** | `top`, `mpstat` | Every 5 minutes |
| **Memory Usage** | `free -m`, `/proc/meminfo` | Every 5 minutes |
| **Disk Usage** | `df -h` | Every 5 minutes |
| **Service Status** | `systemctl is-active nginx` | Every 5 minutes |
| **HTTP Health** | `curl http://server/health` | Every 5 minutes |
| **Nginx Logs** | Ansible fetch | Hourly |

## 🎯 Key Features

- ✅ **Automated Monitoring:** Cron-based health checks every 5 minutes
- ✅ **Centralized Dashboard:** Real-time status via Nginx-served HTML
- ✅ **Log Aggregation:** Ansible collects logs from all app servers
- ✅ **Automated Reporting:** Daily and weekly reports generated automatically
- ✅ **Infrastructure as Code:** Complete Terraform + Ansible automation
- ✅ **Security:** Isolated subnets, security groups, key-based SSH
- ✅ **Scalability:** Easy to add more app servers to monitor

---

## 📂 Repository Structure

```
Project9/
├── README.md
├── .gitignore
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── backend.tf
│   ├── environments/
│   │   ├── dev.tfvars
│   │   ├── staging.tfvars
│   │   └── production.tfvars
│   └── modules/
│       ├── network/
│       ├── monitoring-server/
│       └── app-servers/
├── ansible/
│   ├── ansible.cfg
│   ├── inventory/
│   ├── playbooks/
│   └── roles/
│       ├── nginx-app/
│       ├── monitoring-tools/
│       └── dashboard/
├── scripts/
│   ├── collect-metrics.sh
│   ├── check-services.sh
│   ├── http-health-check.sh
│   ├── build-dashboard.sh
│   └── generate-report.sh
└── docs/
    ├── incident-procedures.md
    └── screenshots/
```
