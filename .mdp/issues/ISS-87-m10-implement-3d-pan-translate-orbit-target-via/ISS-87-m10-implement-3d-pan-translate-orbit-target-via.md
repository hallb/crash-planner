---
id: ISS-87
title: "M10: Implement 3D pan (translate orbit target via middle-mouse or shift+drag)"
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
  - ISS-52
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-11T18:20:43.878Z
updatedAt: 2026-03-11T18:43:30.673Z
---

## Description

Implement pan control for 3D mode. The Phase 10 exit criteria require orbit, **pan**, and zoom. Pan translates the orbit target laterally (perpendicular to the camera view direction), allowing the user to shift the centre of rotation away from the default world centroid.

### Technical approach

- Detect middle-mouse-drag or shift+left-drag when `dimensions == 3`.
- Compute a lateral translation vector in the camera's local right/up plane, scaled by `orbit_distance` for consistent feel at any zoom level.
- Apply the translation to `ViewState.orbit_target`.
- Ensure pan does not fire when the cursor is over imgui panels (`imgui.get_io().want_capture_mouse`).
- 2D pan via `camera_offset` remains unchanged.

### Acceptance criteria

- Middle-mouse-drag (or shift+left-drag) in 3D mode translates the orbit target laterally.
- Pan speed scales with `orbit_distance` so it feels consistent at any zoom level.
- Dragging over imgui panels does not trigger pan.
- 2D pan behaviour is completely unchanged.
- `./script/cibuild` exits 0.

### References

- ISS-52 (ViewState orbit fields — prerequisite)
- Phase 10 exit criteria: "User can orbit, pan, and zoom the 3D viewport"
- FR-001 (3D viewport navigation)