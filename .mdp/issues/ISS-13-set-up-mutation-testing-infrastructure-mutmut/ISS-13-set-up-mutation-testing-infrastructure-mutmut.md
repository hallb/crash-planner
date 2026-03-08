---
id: ISS-13
title: Set up mutation testing infrastructure (mutmut)
type: chore
status: Done
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
updatedAt: 2026-03-08T19:01:56.045Z
---

## Description

Add mutmut to dev deps; configure `[tool.mutmut]` in pyproject.toml (paths: `src/crash/simulation/`, `src/crash/data/`); create `script/mutate`. Per 10-testing-strategy.md.

**Phase exit gate:** Run `script/mutate` after M-2 code is complete; document surviving mutants in M-2 exit log; target ≥70% mutation score on changed Simulation Engine and Data Layer code.

---

## Scoping solution (implementation notes)

How we scope mutation testing to code touched by an issue:

- **Default:** `paths_to_mutate = ["src/crash"]` in `pyproject.toml`; `./script/mutate` mutates the whole package.
- **Per-issue scoping:** `./script/mutate --scope <path1> [path2 ...]` transiently restricts mutations to the given paths. Example: `./script/mutate --scope src/crash/simulation/boids.py`
- **Transient patching:** The script backs up `pyproject.toml`, replaces `paths_to_mutate` and `also_copy` with scoped values, runs mutmut, then restores the original config. No permanent edits.
- **Dynamic also_copy:** `also_copy` is computed from the scope: files in the same dir as scoped paths are listed individually; dirs with no scoped files are added as dirs (for package imports). No manual updates when changing scope.
- **Policy:** Per `testing-policy.mdc`, mutation testing is scoped to code touched by the issue being completed.
