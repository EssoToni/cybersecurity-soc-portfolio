# Current Baseline

Last updated: 2026-11-21

This document records what is actually working in the lab today, what is
installed but not yet validated, and what remains to be done. It supersedes
the Phase 1 draft.

## Already working and verified in Phase 1

- Wazuh manager, indexer and dashboard are running on SIEM-01.
- LNX-ENDPOINT-01 Wazuh agent is Active and forwarding authentication and
  sudo telemetry to SIEM-01.
- WIN-ENDPOINT-01 Wazuh agent is Active and forwarding Windows Security and
  Sysmon telemetry to SIEM-01.
- Host-Only network is operational: all three original VMs communicate with
  SIEM-01 on 192.168.56.0/24.
- Windows telemetry baseline (Day 04) captured and documented.
- Linux telemetry baseline (Day 05) captured and documented.
- Time synchronization verified across SIEM-01 and endpoints.
- Phase 1 telemetry validation checklist is complete.

The previous draft stated "Ubuntu Wazuh agent disconnected". That statement was
stale. The agent is Active and checklist item TV-03 passed. The stale line has
been removed in this version.

## Installed and network-ready, not yet used in a case

- ATTACK-01 is provisioned with Ubuntu Server 24.04 at 192.168.56.40. Hostname
  and the `labattacker` account were confirmed by the operator. It is on the
  Host-Only network, has a clean snapshot, and is not monitored by Wazuh. It
  has not been used to generate any telemetry that a case has consumed.

## Outstanding work

- SOC-001 execution (planned, not started). Depends on ATTACK-01 being used as
  the source and on the safety policy pre-flight checklist being completed.
- Decision on whether ATTACK-01 should become a Wazuh-monitored endpoint. This
  is explicitly out of scope for the current phase. If that changes, the
  architecture, inventory and telemetry validation scope change with it.
- Later phases listed in the README (detection engineering, threat hunting,
  incident response and so on) are not started.
