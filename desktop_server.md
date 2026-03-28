# 🛠️ HomeLab Node: Ryzen 7 Hypervisor
> **Status:** Operational | **Initial Deployment:** March 09, 2026

## 1. System Specifications (BOM)
*This system was acquired with 400 hours of recorded SSD runtime on 09/03/2026.*

| Component       | Model / Specification            | Role / Rationale                         |
| --------------- | -------------------------------- | ---------------------------------------- |
| **CPU** | AMD Ryzen 7 5700X (8C/16T)       | Compute / High-density Virtualization    |
| **Motherboard** | Gigabyte B450 DS3H (Rev 1.0)     | System Backbone (B450 Chipset)           |
| **GPU** | NVIDIA GeForce RTX 3060 Ti (8GB) | AI/Ollama Inference & HW Transcoding     |
| **RAM** | 32GB Crucial Ballistix DDR4-3200 | VM Memory Pool (ECC-non-req)             |
| **Storage** | 1TB Cusu M.2 NVMe SSD            | Boot & VM Storage (LVM-Thin Partitioned) |
| **PSU** | [Add Wattage/Model here]         | Power Delivery                           |
| **Chassis** | 7x RGB Fans + Tower Cooler       | Active Thermal Management                |

---

## 2. Physical & Network Connectivity
* **Management Port:** Onboard Realtek GbE → **Tp-Link Deco X10**.
* **Headless Setup:** No active display output. Management is handled exclusively via **SSH** and **Proxmox Web UI**.

---

## 3. Firmware / BIOS Optimization
*Baseline configuration applied post-CMOS reset to ensure Proxmox stability.*

### A. Performance & Virtualization
* **SVM Mode:** `Enabled` (Required for KVM/Proxmox virtualization).
* **X.M.P. Profile:** `Profile 1` (Ensures RAM stability at 3200MHz vs 2133MHz default).
* **Path:** `M.I.T. > Advanced Memory Settings`.

### B. IOMMU & PCIe Passthrough
*Crucial for passing the RTX 3060 Ti directly to a Linux VM for Ollama/AI workloads.*
* **Above 4G Decoding:** `Enabled`.
* **Re-Size BAR Support:** `Auto`.
* **IOMMU:** `Enabled`.
* **Path:** `Peripherals > AMD CBS > NBIO Common Options`.

---

## 4. Hardware Maintenance & Thermal Log

| Date       | Action                      | Result                            |
| ---------- | --------------------------- | --------------------------------- |
| 09/03/2026 | Initial Build & BIOS Tuning | System POSTs with XMP/SVM active. |
| 28/03/2026 | Documentation Audit         | Verified hardware specs & BIOS.   |

---

## 5. Disaster Recovery (Hardware)
* **BIOS Reset:** Short the `CLR_CMOS` pins or remove the CR2032 battery for 30 seconds.
* **Boot Priority:**
  1. Cusu NVMe (Proxmox Bootloader)
  2. USB Generic (For System Recovery/Re-installs)

---

## 6. Maintenance History
* **09/03/2026**: Initial Build, BIOS Tuning, and OS Installation.
* **28/03/2026**: Updated hardware BOM and documentation for public portfolio.
