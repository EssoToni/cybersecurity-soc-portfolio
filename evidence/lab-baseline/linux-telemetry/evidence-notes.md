# Evidence Notes — Linux Telemetry Baseline 

**Captured:** 2026-10-30
**Endpoint:** LNX-ENDPOINT-01 (sanitized placeholder)  
**Baseline table:** [../../../docs/references/linux-event-baseline-table.md](../../../docs/references/linux-event-baseline-table.md)  
**Resource config:** [../../../docs/references/lab-resource-configuration.md](../../../docs/references/lab-resource-configuration.md)

## Files in this folder

| File | What it shows | Action ref | Sanitized |
|---|---|---|---|
| `screenshots/01-auth-log-review.png` | `auth.log` tail with sshd and sudo lines | Action 1 | Yes |
| `screenshots/02-sudo-activity.png` | `grep sudo` output | Action 1 | Yes |
| `screenshots/03-baseline-auth-activity.png` | Normal SSH and sudo activity | Action 2 | Yes |
| `screenshots/04-baseline-sudo.png` | Normal sudo execution | Action 2 | Yes |
| `screenshots/05-baseline-auditd-execve.png` | `ausearch -m EXECVE` output | Action 2 | Yes |
| `screenshots/06-baseline-listening-sockets.png` | `ss -tulnp` snapshot | Action 2 | Yes |
| `screenshots/07-wazuh-linux-events-visible.png` | Discover showing Linux events | Action 3 | Yes |
| `sample-events/ssh-success.log` | One sanitized SSH success line | Action 2 | Yes |
| `sample-events/sudo-execution.log` | One sanitized sudo line | Action 2 | Yes |

## Sanitization applied
- Real hostname replaced with `LNX-ENDPOINT-01`.
