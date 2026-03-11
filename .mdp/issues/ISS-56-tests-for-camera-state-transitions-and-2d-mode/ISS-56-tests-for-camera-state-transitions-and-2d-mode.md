---
id: ISS-56
title: Tests for camera state transitions and 2D mode regression
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-10
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-52
  - ISS-53
  - ISS-54
  - ISS-55
  - ISS-87
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-11T18:20:21.769Z
    author: M-10-review
    body: "Enriched: added description, test scope, acceptance criteria, and blockedBy ISS-52/53/54/55 during M-10 issue review."
createdAt: 2026-03-09T03:28:06.235Z
updatedAt: 2026-03-11T18:20:57.088Z
---

## Description

Add unit and integration tests covering orbit camera state transitions and verify that 2D mode is unaffected by the new 3D camera code paths.

### Test scope

**Unit tests (camera state):**
- `orbit_yaw` wraps or clamps correctly after full rotation.
- `orbit_pitch` clamps to `[-π/2 + ε, π/2 - ε]`.
- `orbit_distance` clamps to `[min, max]` bounds on scroll.
- Default `orbit_target` resolves to world centroid.
- Setting `orbit_target` to an agent position (follow mode) changes the computed eye position.

**Integration tests (view matrix):**
- Varying yaw produces a camera that orbits horizontally around the target.
- Varying pitch moves the camera vertically around the target.
- Varying distance moves the camera closer/farther along the radial axis.
- The computed eye position matches the expected spherical-to-Cartesian conversion.

**Regression tests (2D mode):**
- With `dimensions == 2`, orbit fields on `ViewState` are ignored.
- 2D pan/zoom via `camera_offset` still functions correctly.
- Existing 2D tests pass without modification.

### Acceptance criteria

- All new tests pass.
- No regressions in existing test suite.
- `./script/cibuild` exits 0.

### References

- ISS-52, ISS-53, ISS-54, ISS-55 (prerequisites — all camera features must exist to test)
- FR-001 (3D viewport navigation)
- Testing policy: unit + integration coverage for new behaviour