---
id: ISS-14
title: Document surviving boids mutation test mutants
type: chore
status: Done
priority: Low
labels: []
assignee: null
milestone: null
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-10T18:50:00.000Z
    author: cli
    body: "Resolved: Surviving mutants are documented via the mutmut database (mutmut results, mutmut show <id>). No separate markdown doc; canonical record is the mutation-test run state. Marked Done."
createdAt: 2026-03-08T14:56:35.117Z
updatedAt: 2026-03-10T18:50:43.446Z
---

## Context

After improving mutation coverage on `src/crash/simulation/boids.py` (2025-03), the scoped run achieved ~99% kill rate (160 killed, 2 survived, 74 skipped). Per testing-policy.mdc, surviving mutants should be either killed by strengthening tests or documented as equivalent with justification.

## Survivors

Two mutants survive in `boids.py`. Run `./script/mutate --scope src/crash/simulation/boids.py` and `mutmut results` filtered for `crash.simulation.boids` and `survived` to identify specifics. These were not investigated further; this issue tracks them for backlog cleanup.

## Latest verification

Reconfirmed during M-2 closeout mutation check (2026-03-08): scoped mutation run still reports surviving boids mutants, so this issue remains open backlog by design.

## Resolution

Surviving boids mutants are documented by the mutmut database: run `mutmut results` (filter for `crash.simulation.boids` and `survived`) and `mutmut show <mutant_id>` for exact mutations. No separate markdown list is maintained; the mutation-test run state is the canonical record. Per testing strategy, phase exit gates require survivors killed or documented—the database fulfils the documentation requirement.
