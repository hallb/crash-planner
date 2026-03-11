---
id: ISS-52
title: Extend ViewState with orbit camera state (yaw, pitch, zoom radius)
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-10
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-11T18:19:43.414Z
    author: M-10-review
    body: "Enriched: added description, technical approach, and acceptance criteria during M-10 issue review."
createdAt: 2026-03-09T03:28:05.844Z
updatedAt: 2026-03-11T18:28:50.183Z
---

## Description

Extend `ViewState` (in `data/state.py`) with orbit camera fields for 3D mode: `orbit_yaw`, `orbit_pitch`, and `orbit_distance`. These store the spherical-coordinate camera state used by the 3D renderer to compute the view matrix.

The orbit target defaults to the world-volume centroid. When follow is enabled in 3D (ISS-80), the orbit target tracks the selected agent instead.

### Technical approach

- Add `orbit_yaw: float = 0.0`, `orbit_pitch: float = 0.3`, `orbit_distance: float = 500.0` to `ViewState`.
- Add `orbit_target: tuple[float, float, float] | None = None` (None → world centroid).
- Document that these fields are ignored when `dimensions == 2`.
- Ensure default values produce a sensible initial 3D viewpoint (slightly elevated, looking at centre).

### Acceptance criteria

- `ViewState` has `orbit_yaw`, `orbit_pitch`, `orbit_distance`, `orbit_target` fields with documented defaults.
- Existing 2D behaviour is unchanged (fields are unused when `dimensions == 2`).
- Existing tests pass without modification.
- `./script/cibuild` exits 0.

### References

- FR-001 (3D viewport navigation)
- `data/state.py` — current `ViewState` definition
- Phase 10 exit criteria in `10-scope-and-phases.md`