---
id: ISS-14
title: Document surviving boids mutation test mutants
type: chore
status: Backlog
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
log: []
createdAt: 2026-03-08T14:56:35.117Z
updatedAt: 2026-03-08T14:56:35.117Z
---

## Context

After improving mutation coverage on `src/crash/simulation/boids.py` (2025-03), the scoped run achieved ~99% kill rate (160 killed, 2 survived, 74 skipped). Per testing-policy.mdc, surviving mutants should be either killed by strengthening tests or documented as equivalent with justification.

## Survivors

Two mutants survive in `boids.py`. Run `./script/mutate --scope src/crash/simulation/boids.py` and `mutmut results` filtered for `crash.simulation.boids` and `survived` to identify specifics. These were not investigated further; this issue tracks them for backlog cleanup.

## Action

- [ ] Run mutmut show on survivor IDs to capture exact mutations
- [ ] Either add tests to kill them or document as equivalent mutants
- [ ] Close this issue when resolved or explicitly deferred
