# Evidence Notes — Telemetry Validation (Phase 1)

**Captured:** 2026-10-27
**Environment:** SIEM-01 (Wazuh manager), WIN-ENDPOINT-01, LNX-ENDPOINT-01
**Checklist:** [../../../docs/telemetry-validation-checklist.md](../../../docs/telemetry-validation-checklist.md)
**Troubleshooting:** [../../../docs/troubleshooting/telemetry-phase1.md](../../../docs/troubleshooting/telemetry-phase1.md)

## Files in this folder

| File | What it shows | Checklist ref | Sanitized |
|------|---------------|---------------|-----------|
| `screenshots/01-wazuh-manager-health.png` | systemctl + wazuh-control output | TV-01 | Yes |
| `screenshots/02-windows-agent-status.png` | agent_control -lc showing Windows agent Active | TV-02 | Yes |
| `screenshots/03-linux-agent-status.png` | agent_control -lc showing Linux agent Active | TV-03 | Yes |
| `screenshots/04-test-event-visible.png` | Discover filtered to eventID 4625 | TV-04 | Yes |
| `sample-events/windows-authentication.json` | Exported 4625 event JSON | TV-04 | Yes |
| `sample-events/linux-authentication.log` | auth.log lines from failed SSH | TV-05 | Yes |

