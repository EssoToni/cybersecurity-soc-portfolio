# Week 01 Review

Week: 2026-10-26 to 2026-11-01 (finalized 2026-11-21)
Phase: 1 - Foundation, environment and public baseline

## Completed

- Repository structure, topic folders and documentation skeleton.
- Phase 1 telemetry validation checklist (Wazuh manager, Windows agent, Linux agent, test events, time sync).
- Windows telemetry baseline (Day 04): audit policy, Event Viewer custom views, 4624 / 4625 / 4688 / account management, cheat sheet, baseline screenshots.
- Linux telemetry baseline (Day 05): auth.log, sudo, auditd, socket baseline, event table, resource config.
- Lab safety policy v1.0, evidence naming convention, SOC case template.
- SOC-001 case scaffold (planned).
- Architecture, resources, inventory, baseline, limitations, README: rewritten for four-VM lab including ATTACK-01.
- Two stale topology PNGs removed, replaced with Mermaid source.

## Hours

- Day 01 to 03 (setup, Wazuh, telemetry validation): approximately 12 hours.
- Day 04 (Windows baseline): approximately 4 hours.
- Day 05 (Linux baseline): approximately 4 hours.
- Day 06 (safety, naming, templates): approximately 3 hours.
- Day 07 (consolidation, architecture pass, README): approximately 3 hours.
- Week 01 total: approximately 26 hours.

## Blockers

- None open. Ubuntu agent connection confirmed Active; stale baseline line removed.
- Wazuh index retention on SIEM-01 is not configured. Tracked in `docs/resources.md` Section 6. Not blocking.

## Next week

- Execute SOC-001 (SSH auth failure simulation against LNX-ENDPOINT-01, source ATTACK-01).
- Capture endpoint and SIEM evidence, build timeline, write verdict.
- Begin detection engineering: tune or write at least one rule based on the SOC-001 findings.
- If time permits, enable Wazuh index retention and record the setting in `lab-resource-configuration.md`.

## Notes

The week's priority was not building detections. It was proving the telemetry pipeline works before any attack runs. A missed detection on a broken log source is not a detection engineering problem, it is a broken baseline. That is the reason Phase 1 exists.
