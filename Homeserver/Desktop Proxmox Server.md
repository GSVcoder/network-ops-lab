## 1. Hardware & BIOS Configuration

### A. Hardware Inventory
* **CPU:** AMD Ryzen 7 5700X (8C / 16T)
* **Motherboard:** Gigabyte B450 DS3H (**Revision 1.0**)
* **GPU:** EVGA RTX 3060 Ti (8GB VRAM)
* **RAM:** 32GB Crucial Ballistix DDR4-3200MHz
* **Storage:** Cusu 1TB M.2 NVMe SSD

### B. Performance & Virtualization (BIOS)
* **SVM Mode:** `Enabled` (Required for KVM/Proxmox virtualization)
* **X.M.P. Profile:** `Profile 1` (Ensures RAM stability at 3200MHz vs 2133MHz default)
* **Path:** `M.I.T. > Advanced Memory Settings`

### C. IOMMU & PCIe Passthrough (BIOS)
* **Above 4G Decoding:** `Enabled`
* **Re-Size BAR Support:** `Auto`
* **IOMMU:** `Enabled`
* **Path:** `Peripherals > AMD CBS > NBIO Common Options`
* *Note: Essential for passing the RTX 3060 Ti directly to a Linux VM for AI workloads.*

---

## 2. ### Physical Network Topology
* **Endpoint:** Proxmox Node
* **Switch:** MikroTik CSS610 Port (`SWITCH_IP`)
* **Router:** MikroTik hAP ax² (`AX2_ROUTER_IP`)
* **Path:** `Proxmox Node` $\rightarrow$ `CSS610 Switch Port` $\rightarrow$ `hAP ax² Router`

---

## 3. System Hardening & Configuration

### A. SSH Hardening (Root Access)
```bash
# Open the SSH configuration file
nano /etc/ssh/sshd_config

# Modify parameters:
PermitRootLogin yes
PasswordAuthentication yes

# Save, exit, and restart the service:
systemctl restart ssh
