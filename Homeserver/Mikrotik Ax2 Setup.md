## Overview & Initial Access

- **Hardware Setup:** Router reset, connected Ethernet cable from Port 1 (WAN) to Port 4 of the NOS Gateway running in bridge mode.
    
- **Management IP:** `AX2_ROUTER_IP` (Renewed IP address to pull the new lease).
    
- **Default Credentials:** `USERNAME` / `PASSWORD` (Immediate password change performed upon first login via WinBox).
    
- **Primary Interface:** **WinBox.exe** (preferred over web UI for its robust interface and theme toggling).
    

## Phase 1: Fiber Gateway Bridge Activation

### MEO FiberGateway Bridge Activation

- **Context:** ISP support was unresponsive; performed a manual override via Telnet to eliminate Double NAT and gain full control over edge routing.
    
- **Windows Prep:** Installed the Telnet client via Administrator Command Prompt: DOS
    
    ```
    dism /online /Enable-Feature /FeatureName:TelnetClient
    ```
    
- **Remote Access:** Connected to the gateway at `telnet MEO_ROUTER_IP` using credentials `ADMIN` / `PASSWORD`.
    
- **Configuration:**
    
    - Enable Command: `lan/bridge-mode/config --enable=enable`
        
    - Verification: Confirmed activation via `lan/bridge-mode/show` and the MEO Web UI.
        

### NOS FiberGateway Bridge Activation

- **Configuration:** Accessed `NOS_ROUTER_IP`, enabled Bridge Mode, and assigned it to **Port 4** of the NOS router to feed the MikroTik hEX / ax2 router.
    

## Phase 2: Mesh Deployment & Topology

- **Deco Configuration:** Switched all TP-Link Deco units to **Access Point (AP) Mode** to ensure the MikroTik remains the sole DHCP server and gateway.
    
- **Physical Links:**
    
    - NOS Port 4 (Bridge) $\rightarrow$ MikroTik Port 1 (WAN)
        
    - MikroTik Port 2 (LAN) $\rightarrow$ Deco X10 (Primary AP)
        
- **Deco Distribution:**
    
    - **Living Room:** Deco X10 (Primary AP connected to MikroTik)
        
    - **UpStairs:** Deco X1500
        

## Phase 3: Initial Setup & OS Lifecycle

- **Access & Security:** Connected via WinBox using the hardware MAC address; immediate password change executed.
    
- **RouterOS Update:** Navigated to **System > Packages** to install the latest software version and rebooted.
    
- **RouterBOARD Firmware:** Upgraded hardware BIOS via **System > RouterBOARD** and performed a manual reboot to sync the hardware with OS version `7.24.2`.
    

## Phase 4: Service Hardening & Networking

- **Attack Surface Reduction:** Navigated to **IP > Services** and disabled insecure services (`FTP`, `WWW`, `API`, `Telnet`). Kept only **WinBox** and **SSH** active.
    
- **WAN Verification:** Confirmed a valid Public IP assignment via **IP > DHCP Client**.
    
- **Wireless Provisioning (WiFi 6):** Configured 2.4GHz and 5GHz radios with **WPA2/WPA3 PSK Mixed Mode**, `20/40/80MHz` channel width, and regulatory domain set to **Portugal**.
    

## Phase 5: Asset Identification & Static Mapping

- **Naming Convention:** Implemented a functional prefix system for the `Comment` field in DHCP Leases to keep track of network endpoints.
    
- **DHCP Reservations:** Converted dynamic leases to Static to ensure permanent IP assignments.
    
- **Identified Devices:**
    
    - **Infrastructure (.2 - .5):** Core network hardware and switches.
        
    - **Personal Workstations (.6 - .7):** Primary desktop and laptop nodes.
        
    - **Mobile & IoT (.8 - .11):** Smartphones, tablets, and smart home devices.
        

## Phase 6: CLI Security Hardening

Executed final security configurations via the internal WinBox Terminal to protect the router from external discovery and exploits:

- **Disable Neighbor Discovery on WAN:**
    
    Plaintext
    
    ```
    /ip neighbor discovery-settings set discover-interface-list=LAN
    ```
    
- **Disable Bandwidth Server:**
    
    Plaintext
    
    ```
    /tool bandwidth-server set enabled=no
    ```
    

## Phase 7: Data Integrity

- **Action:** Generated a Safety Backup to establish a baseline recovery point for this stable configuration and saved it to Google Drive.
    

## Phase 8: Network Layer & Resiliency Automation

Configured automated failover handling to account for the local server environment (running on a laptop that may be powered off).

### DHCP DNS Configuration

- **Primary:** `DOCKER_IP_PIHOLE` (Pi-hole) — Ad-blocking and local domain resolution.
    
- **Secondary:** `1.1.1.1` (Cloudflare) — Emergency upstream internet access.
    

### Netwatch Automation (Failover)

- **Host:** `DOCKER_IP` | **Interval:** `00:01:00`
    
- **Up Script:**
    
    Plaintext
    
    ```
    /ip dhcp-server network set [find address="NETWORK_IP/24"] dns-server=DOCKER_IP,1.1.1.1,NETWORK_IP
    ```
    
- **Down Script:**
    
    Plaintext
    
    ```
    /ip dhcp-server network set [find address="NETWORK_IP/24"] dns-server=1.1.1.1,8.8.8.8
    ```
    
- **Result:** If the server laptop is closed or offline, the router automatically strips the dead Pi-hole IP from the network scope, ensuring uninterrupted internet access for the house.
