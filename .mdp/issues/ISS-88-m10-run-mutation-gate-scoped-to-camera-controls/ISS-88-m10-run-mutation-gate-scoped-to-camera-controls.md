---
id: ISS-88
title: "M10: Run mutation gate scoped to camera controls and view-state code"
type: task
status: Done
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
log:
  - timestamp: 2026-03-11T18:53:47.898Z
    author: M-10-mutmut
    body: |-
      Mutation gate results (scope: state.py, renderer_2d.py, main.py):

      ## Survived — Equivalent Mutants (justified, not killed)

      ### mutmut_34 — intermediate assignment overwritten
      `view_state.trail_buffer = None` (in dim-change clear block) → `""`.
      Observable behavior unchanged: the line is immediately overwritten by
      `view_state.trail_buffer = arr` unconditionally below. Dead intermediate write.

      ### mutmut_38, mutmut_40 — numpy dtype inference
      `np.array(trail_deque, dtype=np.float64)` → `dtype=None` / no-kwarg.
      Numpy infers float64 from Python float lists — identical runtime dtype. Equivalent.

      ### mutmut_41, mutmut_42, mutmut_43, mutmut_44 — dead trail cap code
      `if arr.shape[0] > TRAIL_MAX_LEN: arr = arr[-TRAIL_MAX_LEN:]`
      The deque is constructed with `maxlen=TRAIL_MAX_LEN`, so `arr.shape[0]` ≤ TRAIL_MAX_LEN
      is invariant. This branch can never execute. All four mutations on this block are equivalent.

      ## config_io survivors — pre-existing, outside M-10 scope
      crash.data.config_io.* survivors are pre-existing (not introduced in M-10)
      and are outside the M-10 mutation scope (state.py, renderer_2d.py, main.py).
createdAt: 2026-03-11T18:20:51.825Z
updatedAt: 2026-03-11T18:53:55.220Z
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