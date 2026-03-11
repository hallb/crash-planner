---
id: ISS-88
title: "M10: Run mutation gate scoped to camera controls and view-state code"
type: task
status: In Progress
priority: null
labels: []
assignee: null
milestone: M-10
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-56
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-11T18:20:51.825Z
updatedAt: 2026-03-11T18:50:00.160Z
---

## Description

Run mutation testing scoped to the code touched by M-10 (orbit camera state, input handling for orbit/pan/zoom, view matrix construction, 3D follow wiring). Kill surviving mutants or document them as equivalent.

### Scope

- `data/state.py` (ViewState orbit fields)
- Camera input handling code (orbit, pan, zoom event processing)
- View matrix computation from orbit state
- 3D follow target update logic

### Process

1. All unit and integration tests pass (`./script/test`).
2. Run `./script/mutate --scope <paths>` restricted to the files above.
3. Review surviving mutants:
   - Kill by adding/strengthening tests, or
   - Document as equivalent with justification.
4. `./script/cibuild` exits 0.

### Acceptance criteria

- Mutation testing runs against M-10 scope.
- No unjustified surviving mutants remain.
- `./script/cibuild` exits 0.

### References

- Testing policy: mutation testing runs before milestone completion.
- Prior mutation gates: ISS-13 (M-1), ISS-23 (M-3), ISS-28 (M-4), ISS-43 (M-6), ISS-49 (M-7), ISS-33 (M-9).