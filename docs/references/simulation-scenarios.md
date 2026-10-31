# Simulation Scenario Index

**Purpose:** Track planned, approved and completed lab simulations, in order,
with the rationale for each. Each row links to its case file.

## Rules

- A scenario is only added here once it is scoped in a case file.
- A scenario is only marked `Completed` once evidence is captured and the case
  verdict is recorded.
- Scenarios follow the rules in [../policies/lab-safety.md](../policies/lab-safety.md).

## Scenario list

| Order | Scenario | ATT&CK | Target | Case | Status |
|---|---|---|---|---|---|
| 1 | Repeated authentication failures followed by a successful lab login | T1110 (Brute Force), T1078 (Valid Accounts) | WIN-ENDPOINT-01, LNX-ENDPOINT-01 | [SOC-001](../../investigations/SOC-001-ssh-auth-failure-sim/case.md) | Planned |
| 2 | (future) | | | | |

## Why this scenario is first

1. It requires no tools, no downloads and no elevated privileges to generate.
2. The telemetry it produces (4625, 4624, SSH auth failures, SSH success) is
   already validated in Phase 1 (TV-02 through TV-05).
3. It exercises the full analyst loop: alert → hypothesis → evidence →
   timeline → verdict.
4. It maps cleanly to a real ATT&CK technique, so the case becomes portfolio
   material with minimal tooling risk.

## Scenario-specific safety notes

- **Use a dedicated lab account.** We created `labvictim` (Windows) and
  `labvictim` (Linux) for the simulation.
- **Check the lockout policy first.** Repeated failures can lock an account.
  On the lab target, either we set a high lockout threshold or accept that the lab account will lock and plan to unlock it after the test.
- **Keep the failure count bounded.** A few failures (e.g. 5-10) are enough to
  produce the telemetry. We do not generate hundreds of events : it adds no
  analytical value and makes the timeline noisy.
- **Source host.** The failed attempts originate from ATTACK-01 (or from the
  manager), not from outside the lab.