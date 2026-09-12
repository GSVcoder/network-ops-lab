
### 1. Docker LXC Container Provisioning

- **Target Node:** `NODE` (`DOCKER_IP`)
    
      
    
- **Deployment Tool:** Proxmox VE Community Scripts (Helper-scripts)
    
      
    
- **Execution Command (Shell):**
    
      
    
    Bash
    
    ```
    bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/ct/docker.sh)"
    ```
    
- **Configuration Profile:**
    
      
    - **Install Type:** Advanced
        
          
        
    - **Storage Allocation:** 50GB
        
          
        
    - **Remaining Parameters:** Default container settings
        
          
        

### 2. Portainer Add-on Installation

- **Target Environment:** Newly created Docker LXC container.
    
      
    
- **Execution Command:**
    
      
    
    Bash
    
    ```
    bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/tools/addon/portainer.sh)"
    ```
    

### 3. Management Interface & Access

- **Access URL:** `[https://DOCKER_IP:DOCKER_PORT/](https://DOCKER_IP:DOCKER_PORT/)`
    
      
    
- **Administrative Credentials:**
    
      
    - **Username:** `USERNAME`
        
          
        
    - **Password:** `PASSWORD` _(Stored in Bitwarden vault)_
        
          
        
- **Initial Setup:** Completed administrative bootstrap using the initial setup token extracted directly from the Portainer container logs using the command `docker logs portainer`
