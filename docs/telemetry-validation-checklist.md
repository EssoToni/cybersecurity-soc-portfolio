# Phase 1 — Telemetry Validation Checklist

**Purpose:** Demonstrate that the SOC lab collects the telemetry required for detection and investigation work.
**Scope:** Wazuh manager, Windows endpoint, Linux endpoint, authentication telemetry.
**Environment:** Wazuh 4.x (manager + indexer + dashboard); Windows server VM; Ubuntu server VM.
**Performed:** 2026-10-27
**Executed by:** EssoToni

## Results

| ID    | Validation item                     | Expected result                                     | Actual result | Status | Evidence |
|-------|-------------------------------------|-----------------------------------------------------|---------------|--------|----------|
| TV-01 | Wazuh manager health                | All core daemons running; API responds with error: 0 |All daemons Active; API returned error: 0 | PASS | [01-wazuh-manager-health.png](../evidence/lab-baseline/telemetry-validation/screenshots/01-wazuh-manager-health.png)  |
| TV-02 | Windows agent connection            | Agent status Active in agent_control | Agent active and running; connected to the manager | PASS | [02-windows-agent-status.png](../evidence/lab-baseline/telemetry-validation/screenshots/02-windows-agent-status.png)  |
| TV-03 | Linux agent connection              | Agent status Active in agent_control | Agent active and running; connected to the manager | PASS | [03-linux-agent-status.png](../evidence/lab-baseline/telemetry-validation/screenshots/03-linux-agent-status.png)  |
| TV-04 | Windows authentication telemetry    | Event ID 4625 visible in Wazuh Discover | Event ID 4625 visible in Wazuh Discover | PASS | [04-test-event-visible.png](../evidence/lab-baseline/telemetry-validation/screenshots/04-test-event-visible.png)  [windows-authentication.json](../evidence/lab-baseline/telemetry-validation/sample-events/windows-authentication.json)    |
| TV-05 | Linux authentication telemetry      | Failed SSH auth visible in Wazuh Discover           | Failed SSH auth visible in Wazuh Discover | PASS | [linux-authentication.log](../evidence/lab-baseline/telemetry-validation/sample-events/linux-authentication.log)  |
| TV-06 | Timestamp and hostname verification | Endpoint times synchronized; hostnames unique       | Endpoint times synchronized | PASS | [06-time-check.png](../evidence/lab-baseline/telemetry-validation/screenshots/06-time-check.png)  |
| TV-07 | Evidence preservation               | All items have linked evidence files                | All items have linked evidence files | PASS |          |

**Status values:** PASS / FAIL / BLOCKED / NOT TESTED

## Cross-references
- Troubleshooting log: [troubleshooting/telemetry-phase1.md](troubleshooting/telemetry-phase1.md)
- Evidence folder: [../evidence/lab-baseline/telemetry-validation/](../evidence/lab-baseline/telemetry-validation/)
- Evidence register: [../evidence/evidence-register.csv](../evidence/evidence-register.csv)