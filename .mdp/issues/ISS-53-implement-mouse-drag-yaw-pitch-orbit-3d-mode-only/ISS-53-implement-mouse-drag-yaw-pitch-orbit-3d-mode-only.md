---
id: ISS-53
title: Implement mouse drag → yaw/pitch orbit (3D mode only, mouse events in controls)
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
  - ISS-52
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-11T18:19:51.842Z
    author: M-10-review
    body: "Enriched: added description, acceptance criteria, and blockedBy ISS-52 during M-10 issue review."
createdAt: 2026-03-09T03:28:05.945Z
updatedAt: 2026-03-11T18:30:09.631Z
---

## Description

Implement mouse-drag orbit controls for 3D mode. When `dimensions == 3`, clicking and dragging with the left mouse button (or a designated button/modifier) updates `ViewState.orbit_yaw` and `ViewState.orbit_pitch` based on mouse delta.

### Technical approach

- In the event-handling section of `renderer_2d.py` (or a dedicated input handler), detect mouse drag events when `dimensions == 3`.
- Map horizontal mouse delta → yaw change, vertical mouse delta → pitch change.
- Clamp pitch to avoid gimbal lock (e.g., `[-π/2 + ε, π/2 - ε]`).
- Ensure orbit controls do not fire when the cursor is over the imgui Controls panel (check `imgui.get_io().want_capture_mouse`).
- 2D mode continues to use existing pan/zoom via `camera_offset`.

### Acceptance criteria

- Mouse drag in 3D mode rotates the camera around the orbit target (yaw/pitch).
- Pitch is clamped to prevent flipping.
- Dragging over imgui panels does not trigger orbit.
- 2D mouse behaviour is completely unchanged.
- `./script/cibuild` exits 0.

### References

- ISS-52 (ViewState orbit fields — prerequisite)
- FR-001 (3D viewport navigation)