## MikroTik CSS610-8G-2S+IN Switch Configuration

### 1. Hardware Specifications
* **Model:** MikroTik Cloud Smart Switch (CSS610-8G-2S+IN)
* **Operating System:** SwOS Lite
* **Interfaces:** 8x Gigabit Ethernet ports, 2x SFP+ (10Gbps) ports
* **Power:** DC Jack or PoE-In (Port 1)

### 2. Physical Connectivity & Topology
* **Uplink:** CSS610 Port 1 $\rightarrow$ hAP ax² Port 2 (LAN)
* **Downstream / Distribution:** CSS610 Port 2 $\rightarrow$ Deco Mesh System
* **Proxmox Node Link:** Proxmox Node $\rightarrow$ CSS610 Switch Port $\rightarrow$ hAP ax² Router (`AX2_ROUTER_IP`)

### 3. Management & Access
* **Post-Reset Default Access:** `http://SWITCH_IP/`
* **Credentials:** `USERNAME` / `PASSWORD` *(Immediate password change applied and stored in vault)*

### 4. Network Configuration & Troubleshooting
* **Issue Resolved:** Recovered from a "Connection Refused" state caused by IP conflicts and browser/UI rendering blocks.

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Management IP** | `NETWORK_STATIC_IP` | Assigned via static DHCP reservation on hAP ax² |
| **Fallback IP** | `NETWORK_FALLBACK_IP` | Factory default fallback |
| **Subnet Mask** | `NETWORK_SUBNET_MASK` | Standard Class C |
| **Gateway** | `NETWORK_GATEWAY_IP` | hAP ax² Router |

### 5. Security & Stability Settings
* **Spanning Tree:** RSTP (Rapid Spanning Tree Protocol) enabled globally across all ports to prevent loops and broadcast storms.
* **DHCP Reservation:** MAC address bound explicitly within the hAP ax² router to lock the switch management address permanently at `SWITCH_IP`.
