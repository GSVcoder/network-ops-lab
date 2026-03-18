# Enterprise-Grade Personal Cloud & Networking Lab
A professional-tier homelab environment designed for high-availability service hosting, local AI research, and CompTIA Network+ validation.

## 🏗️ Hardware & Core Infrastructure
* **Hypervisor:** Proxmox VE (LXC & VM Orchestration)
* **Networking:** MikroTik hAP aX2 (Main Router) | MikroTik CSS610 Switch
* **Storage & Backup:** Dedicated Proxmox Backup Server (PBS)
* **Compute:** AMD Ryzen 7 | 8GB VRAM GPU (Optimized for 7B LLM Inference)

## 🌐 Network Services & Security
* **Traffic Management:** **Nginx Proxy Manager** with Cloudflare integration for secure SSL termination.
* **DNS & Ad-blocking:** Redundant **Pi-Hole** instances for network-wide sinkholing.
* **Remote Access:** **Wireguard** VPN for secure, encrypted entry to the internal network.
* **Credential Management:** Self-hosted **Vaultwarden** instance.

## 🚀 Hosted Applications
* **AI Services:** Local AI Server running quantized 7B models.
* **Data & Media:** **Immich** (High-performance photo management) and **Firefly III** (Financial asset tracking).
* **Monitoring:** **Uptime Kuma** for service heartbeat and **Netdata** for real-time hardware telemetry.
* **Dashboard:** Centralized **Homepage** for unified service navigation.

## 🛠️ Dev Ops & Management
* **Containerization:** Docker managed via **Portainer** and custom Docker Stacks.
* **Automation:** Documentation and inventory managed via Obsidian.

