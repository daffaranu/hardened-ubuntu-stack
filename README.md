#  Enterprise-Grade Ubuntu 24.04 LTS Hardened Web Stack

An enterprise-ready, production-hardened Linux web infrastructure designed for high concurrency, zero-trust perimeter defense, and automated disaster recovery.

![Architecture Status](https://img.shields.io/badge/Status-Production--Ready-00FF66?style=for-the-badge)
![OS](https://img.shields.io/badge/Ubuntu-24.04_LTS-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Security](https://img.shields.io/badge/TLS-1.3_Strict-blue?style=for-the-badge)
![Firewall](https://img.shields.io/badge/Firewall-UFW_%2B_Fail2Ban-red?style=for-the-badge)

---

##  Architecture & Core Components

- **Base Operating System:** Ubuntu 24.04 LTS (Minimal attack surface, non-root sudo access, strict kernel sysctl tuning).
- **Reverse Proxy & Web Engine:** Nginx Multi-VirtualHost architecture with OWASP security headers (`HSTS`, `X-Frame-Options`, `X-Content-Type-Options`).
- **Cryptographic Perimeter:** TLSv1.3 modern suite with automated SSL certificate deployment and forward secrecy.
- **Database Isolation:** MariaDB localized strictly to loopback interface `127.0.0.1:3306`, completely invisible from public routing.
- **Active Intrusion Defense:** Stateful UFW perimeter firewall coupled with Fail2Ban IPS monitoring SSH authentication logs.
- **Live Observability:** Endpoint `/api/health.json` tracking system health metrics in real-time (CPU load, RAM consumption, disk usage, service daemons).
- **Disaster Recovery:** Daily automated cron-driven backup daemon with 7-day retention rotation.
- **Autonomous Watchdog:** Bash daemon integrated with Telegram Bot API providing instant failure alerting and automatic service self-healing.

---

##  Live System Telemetry Endpoint

The stack provides an automated health probe reporting real-time node operational status:

```json
{
  "hostname": "production-web-01",
  "services": {
    "nginx": "active",
    "mariadb": "active",
    "fail2ban": "active",
    "ufw": "active"
  }
}
