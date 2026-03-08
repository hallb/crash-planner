---
id: ISS-13
title: Set up mutation testing infrastructure (mutmut)
type: chore
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-2
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T02:30:00.000Z
updatedAt: 2026-03-08T02:30:00.000Z
---

## Description

Add mutmut to dev deps; configure `[tool.mutmut]` in pyproject.toml (paths: `src/crash/simulation/`, `src/crash/data/`); create `script/mutate`. Per 10-testing-strategy.md.

**Phase exit gate:** Run `script/mutate` after M-2 code is complete; document surviving mutants in M-2 exit log; target ≥70% mutation score on changed Simulation Engine and Data Layer code.
