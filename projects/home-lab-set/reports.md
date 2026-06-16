# MULTI-OS OFFENSIVE SECURITY LABORATORY INFRASTRUCTURE SETUP REPORT

**Author:** Cybersecurity Associate / Portfolio Engineering Project  
**Framework Reference:** NIST SP 800-115 Technical Guide to Information Security Testing  
**Document Type:** Lab Architecture & Deployment Blueprint  
**Classification:** Internal — Environment Configuration Records

---

## SECTION 1: LABORATORY OBJECTIVE & ENGINEERING GOALS

The primary engineering objective is to build a fully functional, multi‑operating system penetration testing sandbox using a single physical host machine. The lab is designed to support safe, ethical, and controlled execution of network reconnaissance, vulnerability scanning, and exploitation workflows without exposing production assets or external networks to risk.

By deploying a Type‑2 hypervisor with a Bridged Network topology, the environment replicates an on‑site internal network audit scenario. This setup provides a stable platform for practicing offensive security techniques, examining legacy service vulnerabilities, and documenting proof‑of‑concept attacks.

---

## SECTION 2: HOST HARDWARE & HYPERVISOR CONFIGURATION

Stable operation under multi‑threaded scanning loads requires careful partitioning of physical compute resources between the host operating system and guest virtual machines.

- **Host Operating System:** Microsoft Windows 10 / Windows 11 Enterprise (64‑bit)
- **Hypervisor:** Oracle VM VirtualBox v7.x (Type‑2 Hosted Virtualization)
- **Hardware Virtualization Extensions:** Intel VT‑x / AMD‑V enabled in UEFI/BIOS firmware
- **Resource Allocation Strategy:**
  - **Host Margin:** Minimum 4 GB RAM reserved for Windows background services and UI responsiveness
  - **Guest Pools:** Virtual machines receive thin‑provisioned virtual disks and dedicated RAM slices to avoid memory contention

---

## SECTION 3: NETWORK TOPOLOGY — BRIDGED MODE DESIGN

The lab employs a Layer‑2 hardware bridge via the VirtualBox NDIS6 Bridged Networking Driver. This filter driver attaches directly to the host laptop's active physical network adapter (Ethernet or Wi‑Fi), enabling guest machines to appear as independent nodes on the local router's subnet.

