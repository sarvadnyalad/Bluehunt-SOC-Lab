# BlueHunt SOC Lab — Setup Guide

## Day 1 — Lab Setup & Log Ingestion
1. **Virtualization & Hypervisor**
   - Enable VT‑x/AMD‑V in BIOS/UEFI.
   - Install VirtualBox.
2. **VMs & Networking**
   - Create **Kali** (2 GB RAM, 2 vCPU, 30 GB) and **Windows 10/11** (4–6 GB RAM, 2 vCPU, 40 GB).
   - Two adapters each: **Adapter 1: NAT**, **Adapter 2: Internal Network `LABNET`**.
   - Assign static IPs on Internal NICs:
     - Kali `10.10.10.10/24`
     - Windows `10.10.10.20/24`
   - Enable Windows ICMP inbound rule and verify ping both ways.
3. **Windows Telemetry**
   - Install **Sysmon** with a known-good config (e.g., SwiftOnSecurity).
   - Enable **PowerShell Script Block** + **Module** logging via `gpedit.msc`.
4. **Defender for Endpoint (MDE)** *(in progress)*
   - Create/confirm tenant, download **Windows onboarding package**, run the script (Sense service running).
5. **Azure & Sentinel**
   - Create **Log Analytics Workspace** and enable **Microsoft Sentinel**.
   - Onboard Windows to **Azure Arc**, install **Azure Monitor Agent (AMA)**.
   - Create a **Data Collection Rule** for **Security**, **System**, **Application**, and **Microsoft-Windows-Sysmon/Operational**.
6. **Verify Ingestion (KQL)**
   - `Heartbeat | take 5`
   - `Event | take 5`
   - `Event | where Source == "Microsoft-Windows-Sysmon" | take 5`
   - `SecurityEvent | take 5` (after Security Events via AMA)

## Day 2 — Simulate Attacks & Detect (still in progress)
- Run nmap scan, hydra RDP brute force (optional), EICAR, and encoded PowerShell.
- Hunt with KQL and convert hunts into Analytic Rules.

## Day 3 — Report & Finalize (still in progress)
- Write incident reports with evidence.
- Build a Sentinel workbook dashboard.
- Final verification run.
