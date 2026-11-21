# Lab Topology

Rendered on GitHub from the Mermaid source below. To regenerate a PNG, paste
the same source into mermaid.live.

```mermaid
graph LR
  subgraph HOST["Windows 11 workstation (SOC Analyst)"]
    host["192.168.56.1<br/>VirtualBox + Wireshark + GitHub"]
  end

  subgraph LAB["VirtualBox Host-Only network 192.168.56.0/24"]
    siem["SIEM-01<br/>192.168.56.10<br/>Wazuh manager, indexer, dashboard"]
    lnx["LNX-ENDPOINT-01<br/>192.168.56.20<br/>Ubuntu Server 24.04<br/>Wazuh agent"]
    win["WIN-ENDPOINT-01<br/>192.168.56.30<br/>Windows Server 2019<br/>Wazuh agent, Sysmon"]
    atk["ATTACK-01<br/>192.168.56.40<br/>Ubuntu Server 24.04<br/>Simulation source (unmonitored)"]
  end

  host -- "HTTPS 443 / API 55000" --> siem
  lnx -- "Wazuh agent 1514/tcp" --> siem
  win -- "Wazuh agent 1514/tcp" --> siem
  atk -. "simulation traffic, endpoints only" .-> lnx
  atk -. "simulation traffic, endpoints only" .-> win

  note["No external route during simulations.<br/>NAT attached for maintenance only, detached before any simulation."]
  LAB --- note
```

Legend

    Solid line: lab monitoring traffic.

    Dashed line: simulation traffic.

    The note records the isolation constraint from
    docs/policies/lab-safety.md
