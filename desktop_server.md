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
