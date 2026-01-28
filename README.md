# Infrastructure Monitoring (Uptime Kuma)

This directory contains the deployment configuration for **Uptime Kuma**, a self-hosted monitoring tool used to track the status of my personal infrastructure (Web, Mail, DNS).

- Public access: `https://status.roger.tw`
- Dashboard: `https://status.roger.tw/dashboard`

## Architecture Overview

The monitoring stack is decoupled from the main application stack (`my-portfolio`) to ensure reliability.

- **OS**: Ubuntu Linux
- **Container Runtime**: Docker & Docker Compose
- **Security**: UFW, Fail2Ban, Internal Binding (127.0.0.1)
- **Reverse Proxy**: Nginx (handling SSL termination)

### Directory Structure

```text
/home/roger/
├── my-portfolio/         # Main Application Layer
│   └── docker-compose.yml
└── infra-monitor/        # Infrastructure Layer (You are here)
    ├── docker-compose.yml
    └── uptime-kuma-data/ # Persistent data volume
```

## Deployment

use `docker-compose.yml` to deploy Uptime Kuma: `docker-compose up -d`

## Security Measures

- Localhost binding: Uptime Kuma listens on `127.0.0.1` to prevent direct external access.
- Reverse Proxy: Nginx handles SSL termination and external access.
    - set `bind9` first
    - set `nginx` for reverse proxy
    - `certbot sudo certbot --nginx -d status.roger.tw`
- 2FA: Enabled for Uptime Kuma for added security.
- Firewall: `ufw` blocks unwanted access.
