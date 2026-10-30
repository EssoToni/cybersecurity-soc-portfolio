# Evidence Notes — Windows Telemetry Baseline 

**Captured:** 2026-10-29  
**Endpoint:** WIN-ENDPOINT-01 (sanitized placeholder)  
**Cheat sheet:** [../../docs/references/windows-event-cheat-sheet.md](../../docs/references/windows-event-cheat-sheet.md)

## Files in this folder

| File | What it shows | Checklist ref | Sanitized |
|---|---|---|---|
| `screenshots/01-event-viewer-auth-custom-view.png` | Custom View filtered to 4624/4625 | Action 1 | Yes |
| `screenshots/02-event-viewer-process-custom-view.png` | Custom View filtered to 4688 | Action 1 | Yes |
| `screenshots/03-baseline-auth-events.png` | Normal logon activity (Type 2, Type 7) | Action 3 | Yes |
| `screenshots/04-baseline-process-creation.png` | `cmd.exe` → `whoami.exe` parent–child chain | Action 3 | Yes |
| `screenshots/05-baseline-account-management.png` | 4720 and 4726 from test account | Action 3 | Yes |
| `sample-events/4624-interactive-logon.xml` | Raw XML of a 4624 event | Action 2 | Yes |
| `sample-events/4688-cmd-execution.xml` | Raw XML of a 4688 event with command line | Action 2 | Yes |

## Sanitization applied
- Real computer name replaced with `WIN-ENDPOINT-01`.
