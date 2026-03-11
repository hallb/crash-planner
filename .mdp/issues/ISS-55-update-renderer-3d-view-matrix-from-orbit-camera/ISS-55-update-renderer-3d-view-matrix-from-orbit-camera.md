---
id: ISS-55
title: Update renderer 3D view matrix from orbit camera state
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
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-11T18:20:12.323Z
    author: M-10-review
    body: "Enriched: added description, technical approach, acceptance criteria, and blockedBy ISS-52 during M-10 issue review."
createdAt: 2026-03-09T03:28:06.137Z
updatedAt: 2026-03-11T18:20:12.323Z
---

## Description

Wire the orbit camera state from `ViewState` into the 3D rendering path so the view matrix reflects `orbit_yaw`, `orbit_pitch`, `orbit_distance`, and `orbit_target`.

### Technical approach

- In the 3D branch of the render method (currently in `renderer_2d.py`), compute the camera position from spherical coordinates:
  ```
  eye.x = target.x + distance * cos(pitch) * sin(yaw)
  eye.y = target.y + distance * cos(pitch) * cos(yaw)
  eye.z = target.z + distance * sin(pitch)
  ```
- Build a look-at view matrix from `eye` → `target` with an appropriate up vector.
- Replace the current hard-coded 3D camera position with this computed eye position.
- When `orbit_target` is None, default to world-volume centroid `(w/2, h/2, d/2)`.

### Acceptance criteria

- 3D view matrix is derived from `ViewState` orbit fields, not hard-coded.
- Changing `orbit_yaw`, `orbit_pitch`, `orbit_distance` produces the expected camera movement.
- Default orbit state renders a view equivalent to (or better than) the current hard-coded 3D camera.
- 2D rendering path is completely unchanged.
- `./script/cibuild` exits 0.

### References

- ISS-52 (ViewState orbit fields — prerequisite)
- FR-001 (3D viewport navigation)
- `renderer_2d.py` — current 3D view matrix construction