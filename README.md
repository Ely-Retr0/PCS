#  PCS — Portable Cloud Server

> *A Raspberry Pi as a command-and-control server that manages containers locally and offloads heavy workloads to Oracle Cloud Free Tier — self-sustaining cloud infrastructure in your pocket.*

![Status](https://img.shields.io/badge/status-in%20development-dc143c?style=flat-square)
![Hardware](https://img.shields.io/badge/hardware-Raspberry%20Pi-C51A4A?style=flat-square)
![Stack](https://img.shields.io/badge/stack-Docker%20%7C%20K8s%20%7C%20Terraform-ff6a00?style=flat-square)
![License](https://img.shields.io/badge/license-MIT-39ff14?style=flat-square)

---

## What is PCS?

PCS (Portable Cloud Server) turns a **Raspberry Pi** into a self-sustaining C2 (command and control) node for a hybrid cloud infrastructure. The Pi manages containers and services locally via Docker, Kubernetes, and Terraform — and intelligently delegates compute-heavy tasks to **Oracle Cloud Free Tier**, which provides always-free VM instances.

The result: a fully functional, portable cloud that costs **$0/month** to run.

---

## Architecture

```
┌──────────────────────────────────────────────────────┐
│                 Raspberry Pi (C2 Node)               │
│                                                      │
│  ┌────────────┐  ┌────────────┐  ┌───────────────┐  │
│  │  Docker    │  │ Kubernetes │  │   Terraform   │  │
│  │ Containers │  │ Orchestrat │  │ Infrastructure│  │
│  └────────────┘  └────────────┘  └───────┬───────┘  │
│                                          │           │
│  Light tasks run locally on the Pi       │           │
└──────────────────────────────────────────┼───────────┘
                                           │ delegates heavy workloads
                                           ▼
┌──────────────────────────────────────────────────────┐
│              Oracle Cloud Free Tier                  │
│                                                      │
│  • 2x AMD VM (1 OCPU, 1GB RAM each) — Always Free   │
│  • 4x ARM VM (24GB RAM total) — Always Free          │
│  • Object Storage — Always Free                      │
│  • Load Balancer — Always Free                       │
│                                                      │
│  Heavy compute, storage, and services run here       │
└──────────────────────────────────────────────────────┘
```

---

## Why This Architecture?

- **Pi is lightweight C2** — low power, always on, manages everything
- **Oracle Free Tier is the muscle** — actual compute happens in the cloud
- **Terraform manages both** — single IaC layer for Pi-local and cloud resources
- **Kubernetes orchestrates containers** — across Pi and cloud nodes
- **Cost: $0/month** — Oracle Free Tier is genuinely free forever

---

## Features

- 🐳 Docker container management on the Pi
- ☸️ Kubernetes cluster spanning Pi + Oracle Cloud nodes
- 🏗️ Terraform for infrastructure-as-code (IaC)
- ☁️ Oracle Cloud Free Tier integration
- 📊 Web dashboard for monitoring all resources
- 🔒 Wireguard VPN tunnel between Pi and cloud
- 🔋 Portable — works anywhere with internet access
- 💰 $0/month infrastructure cost

---

## Services You Can Run

| Service | Where |
|---|---|
| Reverse proxy (Nginx/Caddy) | Pi |
| Personal VPN (Wireguard) | Oracle Cloud |
| File storage (Nextcloud) | Oracle Cloud |
| Password manager (Vaultwarden) | Oracle Cloud |
| Monitoring (Grafana + Prometheus) | Pi + Cloud |
| CI/CD pipeline | Oracle Cloud |
| Personal website / portfolio | Oracle Cloud |

---

## Requirements

### Hardware
- Raspberry Pi 4 (4GB+ recommended)
- 32GB+ microSD
- Stable internet connection

### Accounts (Free)
- Oracle Cloud account (free tier)
- Domain name (optional, for custom URLs)

### Software
- Docker & Docker Compose
- Kubernetes (k3s — lightweight)
- Terraform
- Wireguard

---

## Quick Start

```bash
git clone https://github.com/Ely-Retr0/PCS
cd PCS

# 1. Configure your Oracle Cloud credentials
cp config/oracle.example.yml config/oracle.yml
nano config/oracle.yml

# 2. Deploy infrastructure
terraform init
terraform apply

# 3. Start the Pi C2 node
sudo ./scripts/start-c2.sh

# 4. Access dashboard
# http://<your-pi-ip>:8080
```

---

## Roadmap

- [ ] Terraform Oracle Cloud modules
- [ ] k3s cluster setup scripts
- [ ] Wireguard auto-config
- [ ] Web dashboard
- [ ] Auto-scaling logic (Pi → Cloud offload)
- [ ] Backup & recovery automation
- [ ] CLI management tool

---

## Author

**Elias Diaz Gutierrez** — [@Ely-Retr0](https://github.com/Ely-Retr0)  
*Think outside the fierrewall*
