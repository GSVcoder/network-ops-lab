

### 1. Hardware Inventory

- **CPU:** AMD Ryzen 7 5700X (8C / 16T)
    
      
    
- **Motherboard:** Gigabyte B450 DS3H (**Revision 1.0**)
    
      
    
- **GPU:** EVGA RTX 3060 Ti (8GB VRAM)
    
      
    
- **RAM:** 32GB Crucial Ballistix DDR4-3200MHz
    
      
    
- **Storage:** Cusu 1TB M.2 NVMe SSD
    
      
    

### 2. Installation & Network Topology

- **Deployment Method:** Graphical installer (installed without Wi-Fi, static IP configurations applied during setup).
    
      
    
- **Physical Relocation:** Moved downstairs post-installation and connected directly downstream of the core switch.
    
      
    
- **Network Path:** Node $\rightarrow$ CSS610 Switch Port $\rightarrow$ hAP ax² Router (`AX2_ROUTER_IP`).
    
      
    
- **Management Access:** `[https://PROXMOX_IP:PROXOX_PORT](https://PROXMOX_IP:PROXOX_PORT)` (Accessible locally via MikroTik Wi-Fi/Ethernet).
    
      
    
- **Default Credentials:**
    
      
    - **Username:** `USERNAME`
        
          
        
    - **Password:** `PASSWORD`
        
          
        

### 3. System Hardening & Configuration

#### A. SSH Hardening (Enabling Root Access)

Updated the SSH daemon configuration to allow direct administrative access:

  

Bash

```
# Open the SSH configuration file
nano /etc/ssh/sshd_config

# Modify parameters:
PermitRootLogin yes
PasswordAuthentication yes

# Save, exit, and restart the service:
systemctl restart ssh
```

#### B. Repository Management & Trixie Upgrades

Corrected upstream repository sources to clear authorization errors and align with the target build:

  

Bash

```
# 1. Disable Enterprise repositories causing 401 errors
sed -i 's/^deb/#deb/g' /etc/apt/sources.list.d/pve-enterprise.list
sed -i 's/^deb/#deb/g' /etc/apt/sources.list.d/ceph.list

# 2. Remove conflicting local installation lists
rm -f /etc/apt/sources.list.d/pve-install-repo.list

# 3. Register No-Subscription repositories
echo "deb http://download.proxmox.com/debian/pve trixie pve-no-subscription" > /etc/apt/sources.list.d/pve-no-sub.list
echo "deb http://download.proxmox.com/debian/ceph-squid trixie no-subscription" > /etc/apt/sources.list.d/ceph-no-sub.list

# 4. Sync packages and upgrade the system
apt update && apt dist-upgrade -y
```

### 4. Final Validation

- **Network Baseline:** Web UI operational at `PROXMOX_IP:PROXOX_PORT`.
    
      
    
- **Virtualization Readiness:** IOMMU and SVM virtualization extensions verified active via kernel logs (`dmesg`), priming the node for hardware passthrough (RTX 3060 Ti).
    
      
    
- **Package Status:** Repository mirrors synchronized successfully with zero error codes.
