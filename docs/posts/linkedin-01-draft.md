# LinkedIn Post 01 (draft)

Status: draft
Target: Week 01 public signal
Length target: under 1300 characters

---

Most home SOC labs fail because the telemetry lies.

I spent the first week of my SOC portfolio lab not building detections, not running attacks, and not writing rules. I spent it proving the pipeline actually works.

Four VMs on one 12 GB host. Wazuh 4.14.9 on Ubuntu. Windows Server 2019 with Sysmon. Ubuntu Server endpoint. A fourth Ubuntu VM reserved as the simulation source.

Before touching any of them with an attack, I confirmed:

- The Wazuh manager, indexer and dashboard were healthy.
- Windows and Linux agents were Active, not just installed.
- Timestamps were synchronized across every host.
- A real 4625 (failed Windows logon) and a real failed SSH login both arrived in the SIEM.
- The 4688 events actually contained command lines, not just process names.

Why bother?

Because a missed alert on a broken log source is not a detection problem. It is a baseline problem wearing a detection problem's clothes. Every hour spent debugging a "failed detection" that was really a stopped agent is wasted.

Detection engineering on unverified telemetry is expensive guessing.

Next week: the first actual simulation. Then the first detection.

Repo in the comments.

#SOC #DetectionEngineering #Wazuh #BlueTeam
