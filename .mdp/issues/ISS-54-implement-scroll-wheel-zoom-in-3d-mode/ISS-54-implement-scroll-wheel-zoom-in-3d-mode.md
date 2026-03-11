---
id: ISS-54
title: Implement scroll-wheel zoom in 3D mode
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
log:
  - timestamp: 2026-03-11T18:19:58.146Z
    author: M-10-review
    body: "Enriched: added description, acceptance criteria, and blockedBy ISS-52 during M-10 issue review."
createdAt: 2026-03-09T03:28:06.041Z
updatedAt: 2026-03-11T18:43:30.571Z
---

## Description

Implement scroll-wheel zoom for 3D mode. When `dimensions == 3`, scroll events adjust `ViewState.orbit_distance` to move the camera closer to or farther from the orbit target.

### Technical approach

- In the event-handling section, detect `MOUSEWHEEL` events when `dimensions == 3`.
- Map scroll delta to `orbit_distance` adjustment (multiplicative scaling, e.g., `distance *= 0.9` per scroll tick for zoom-in).
- Clamp `orbit_distance` to a sensible range (e.g., `[50, 5000]`) to prevent the camera from entering the flock or zooming too far out.
- Ensure scroll events over imgui panels are consumed by imgui and do not trigger zoom (`imgui.get_io().want_capture_mouse`).
- 2D scroll-wheel behaviour (existing zoom) is unchanged.

### Acceptance criteria

- Scroll wheel zooms in/out in 3D mode by adjusting `orbit_distance`.
- Zoom is clamped to min/max bounds.
- Scrolling over imgui panels does not trigger 3D zoom.
- 2D scroll zoom is unchanged.
- `./script/cibuild` exits 0.

### References

- ISS-52 (ViewState orbit fields — prerequisite)
- FR-001 (3D viewport navigation)