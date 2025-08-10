# BlueHunt SOC Lab

A compact, three‑day Microsoft‑centric SOC lab you can run locally: Kali (attacker) + Windows 10/11 (victim) on an isolated VirtualBox network, with telemetry flowing into Microsoft Sentinel. This repo tracks setup steps, KQL hunts, detections, and incident write‑ups.

## Architecture (Day 1 status)
- VirtualBox host with **two VMs**:
  - **Kali** (attacker): NAT + Internal `LABNET` (10.10.10.0/24)
  - **Windows 10/11** (victim): NAT + Internal `LABNET`
- Telemetry on Windows:
  - **Sysmon** (SwiftOnSecurity config) + **PowerShell logging**
  - **Microsoft Defender for Endpoint (MDE)** onboarding (in progress)
- Cloud side:
  - **Azure Log Analytics Workspace** with **Microsoft Sentinel** enabled
  - **Azure Arc + Azure Monitor Agent (AMA)** + **Data Collection Rule (DCR)** to send **Security**, **System**, **Application**, and **Microsoft-Windows-Sysmon/Operational** logs

## Repo Layout
```
bluehunt-soc-lab/
├─ kql-queries/           # Saved KQL hunts and analytic rule sources
├─ incident-reports/      # Day 2–3 incident write-ups + screenshots
├─ screenshots/           # UI captures from Sentinel/MDE/Portal
├─ setup-guide.md         # Step-by-step guide (Day 1–3)
└─ README.md              # This overview
```

## Quick Start
1. Clone this repo.
2. Follow **setup-guide.md** for Day 1–3 steps.
3. Use **kql-queries/** during hunting and convert useful ones into Analytic Rules in Sentinel.
4. Document findings in **incident-reports/** (one Markdown per incident) and drop evidence into **screenshots/**.

## Current Status (End of Day 1 target)
- [x] Kali & Windows VMs created (NAT + Internal `LABNET`)
- [x] Static IPs: Kali `10.10.10.10`, Windows `10.10.10.20`; ping works
- [x] Sysmon installed; PowerShell logging enabled
- [ ] MDE onboarded (in progress)
- [x] Sentinel workspace ready; Arc + AMA + DCR connected
- [x] Logs visible in **Heartbeat** and **Event** (Sysmon under Event.Source == "Microsoft-Windows-Sysmon")
- [ ] **SecurityEvent** table populated (appears after Windows Security Events via AMA and activity)

## License
MIT