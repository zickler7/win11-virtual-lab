# win11-virtual-lab
Deployment, resource optimization, and troubleshooting of a Windows 11 virtualized environment on UTM hypervisor for 1st Line IT Support competency practice
# 🖥️ Windows 11 Virtual Lab Deployment & Troubleshooting Guide

## 📌 Project Overview
This project documents the end-to-end setup, resource management, and deployment of a virtualized **Windows 11 Pro** environment running on **UTM Hypervisor** (macOS x64 host architecture). Built as a hands-on home lab to demonstrate core **1st Line IT Support / Service Desk Analyst** competencies, including OS provisioning, hypervisor management, disk partition strategy, and host-level troubleshooting.

---

## 🛠️ System Specifications & Architecture
* **Host Machine:** MacBook Pro (x64 Intel Architecture)
* **Host Operating System:** macOS
* **Hypervisor:** UTM (QEMU-based virtualization)
* **Guest Operating System:** Windows 11 Pro (x64)
* **Provisioned Resources:**
  * **vCPU:** 4 Cores
  * **RAM:** 4096 MB (4 GB)
  * **Virtual Disk Allocation:** 28 GB (Optimized dynamic storage)

---

## 🚀 Step-by-Step Installation Process

1. **Hypervisor Configuration:**
   * Configured UTM virtualization profile for Windows 10/11 x64 architecture.
   * Mounted the Windows 11 Installation Media (`.iso`).
   * Booted into UEFI Boot Manager (`UEFI QEMU DVD-ROM`) to initiate OS installation.

2. **OS Setup & Licensing:**
   * Executed clean installation workflow (`Custom: Install Windows only`).
   * Selected targeted partition layout for initial deployment.

---

## 🛑 Troubleshooting & Incident Resolution

### Incident Report #001: Hypervisor Storage Allocation Failure
* **Symptom:** OS setup crashed mid-installation with error message:
  > `QEMU error: #block715: No space left on device`
* **Root Cause Analysis:** 
  * The initial VM configuration allocated a **64 GB** virtual disk. 
  * Although UTM uses dynamic disk expansion, the total size exceeded the physical host machine's available storage space (~25.98 GB available). During Windows setup file extraction, the host disk reached 100% capacity, causing QEMU engine failure.

* **Remediation & Escalation Steps:**
  1. **Host Storage Audit:** Audited host drive space via `System Settings > Storage` to identify high-capacity directories.
  2. **Storage Management:** Unlinked local Messages/iCloud attachment synchronization to safely purge local cache data without impacting user cloud backups.
  3. **VM Re-provisioning:** Terminated the failing VM instance and deleted the oversized 64 GB virtual disk file.
  4. **Right-Sizing Storage:** Created a lean **28 GB** virtual disk allocation to provide necessary headroom for Windows 11 installation while preserving host system stability.
  5. **Clean Partitioning:** Executed partition table wiped via Windows Setup, selecting the new unallocated space to complete deployment.

---

## 🎯 1st Line IT Competencies Demonstrated
* **Virtualization Management:** Hypervisor setup, ISO mounting, hardware resource allocation.
* **Storage & Resource Optimization:** Disk provisioning, dynamic vs. fixed allocation understanding, host storage management.
* **Technical Problem Solving:** Diagnosing low-level QEMU errors, identifying root cause, and executing remediations.
* **Technical Documentation:** Maintaining structured Knowledge Base (KB) articles and incident handling logs using Markdown.

---

## 🔮 Next Lab Objectives
- [ ] Install SPICE Guest Tools for display scaling and guest driver integration.
- [ ] Practice Local User Account Management and RBAC via Command Line (`net user`) and PowerShell.
- [ ] Deploy Remote Server Administration Tools (RSAT) for Active Directory testing.
- [ ] Practice standard network diagnostic scripts (`ipconfig`, `ping`, `nslookup`, `tracert`).
