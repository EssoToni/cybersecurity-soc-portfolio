# Cybersecurity / SOC Analyst Portfolio

Hands-on SOC lab portfolio demonstrating practical work in:

- Security monitoring
- SIEM analysis
- Detection engineering
- Incident investigation
- Threat hunting
- Network analysis
- Vulnerability management
- Security automation

Primary technologies: Wazuh, Windows Server 2019, Ubuntu Server 24.04,
Wireshark, Python, PowerShell, Bash, Sysmon, MITRE ATT&CK.

## Lab at a glance

A single-host VirtualBox lab on an isolated Host-Only network
(192.168.56.0/24). Four VMs plus the Windows 11 workstation that hosts them.

| Host | Role |
|---|---|
| Windows 11 | SOC Analyst workstation (VirtualBox, Wireshark, GitHub) |
| SIEM-01 | Wazuh manager, indexer, dashboard |
| LNX-ENDPOINT-01 | Linux endpoint (Wazuh agent) |
| WIN-ENDPOINT-01 | Windows endpoint (Wazuh agent and Sysmon) |
| ATTACK-01 | Controlled simulation source |

The lab is resource-constrained and runs VMs in combination rather than all at
once. See [docs/resources.md](docs/resources.md) and
[docs/limitations.md](docs/limitations.md).

Simulations are performed only against lab VMs the owner controls, inside the
isolated Host-Only network. See
[docs/policies/lab-safety.md](docs/policies/lab-safety.md).

## Current phase

Phase 1 (Foundation, environment and public baseline).

- Telemetry validation checklist: complete
- Windows telemetry baseline: complete
- Linux telemetry baseline: complete
- SOC-001 case (SSH authentication failure simulation): planned
- ATTACK-01: installed, not yet used in a live case

## Investigations

Cases are tracked under `investigations/` using the `SOC-NNN` naming convention.

| ID | Title | Status |
|---|---|---|
| SOC-001 | SSH auth failure followed by successful lab login | Planned |

Later phases will produce additional cases in the areas of brute force,
suspicious PowerShell, network port scan, suspicious process execution,
phishing, vulnerability assessment, threat hunting and SOC automation. They
will be added as work is completed, not before.

## Documentation

- [Architecture](docs/architecture.md)
- [Lab Topology (Mermaid)](docs/diagrams/lab-topology.md)
- [Asset Inventory](docs/asset-inventory.md)
- [Baseline Status](docs/baseline-status.md)
- [Resource Overview](docs/resources.md)
- [Lab Resource Configuration](docs/references/lab-resource-configuration.md)
- [Limitations](docs/limitations.md)
- [Telemetry Validation Checklist](docs/telemetry-validation-checklist.md)
- [Lab Safety and Rules of Engagement](docs/policies/lab-safety.md)
- [Evidence Naming Convention](docs/references/evidence-naming-convention.md)
- [SOC Case Template](docs/templates/soc-case-template.md)
- [Windows Event Cheat Sheet](docs/references/windows-event-cheat-sheet.md)
- [Linux Baseline Table](docs/references/linux-event-baseline-table.md)
- [Simulation Scenarios](docs/references/simulation-scenarios.md)
- [Phase 1 Troubleshooting](docs/troubleshooting/telemetry-phase1.md)

## Evidence handling

Evidence in this repository is one of three kinds:

- Original evidence, captured from the actual lab, kept local and unmodified.
- Sanitized evidence, derived from original, with sensitive values redacted or
  replaced. Published after review.
- Synthetic evidence, deliberately generated for demonstrations or detection
  tests. Always labelled as synthetic.

See [docs/references/evidence-naming-convention.md](docs/references/evidence-naming-convention.md)
and [docs/policies/lab-safety.md](docs/policies/lab-safety.md) Section 3.

## Notes on this portfolio

This is a learning lab, not a production SOC. Findings, timelines and verdicts
are scoped to the lab environment described here. Nothing in this repository
should be read as production experience.
