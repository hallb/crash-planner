---
id: ISS-79
title: Follow — centre-third dead zone for both 2D and 3D modes
type: bug
status: Backlog
priority: Medium
labels: []
assignee: null
milestone: null
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo:
  - ISS-58
checklist: []
log:
  - timestamp: 2026-03-09T22:00:00.000Z
    author: human-gate
    body: "Human Gate (M-5): Current behaviour fixes bird in centre of viewport. Intent was centre-third dead zone — camera does not move until bird reaches edge of centre third, reducing camera jitter."
  - timestamp: 2026-03-11T18:19:21.377Z
    author: M-10-review
    body: "Moved out of M-10: this is a 2D follow UX bug (centre-third dead zone), unrelated to 3D camera controls. Should be addressed in a dedicated follow-improvement or bug-fix scope."
createdAt: 2026-03-09T22:00:00.000Z
updatedAt: 2026-03-11T19:21:52.313Z
---

## Origin

- **Found during**: M-5 Human Gate (viewport follow verification), confirmed in M-10 Human Gate (3D)
- **Related**: ISS-58 (viewport follow implementation), ISS-80 (3D follow fix)

## Description

**Current behaviour (2D)**: Camera keeps the selected agent pinned to the centre of the viewport.

**Current behaviour (3D)**: `orbit_target` is set directly to agent position each tick — agent is always at the centre of the orbit.

**Intended behaviour (both modes)**: Use a **centre-third dead zone**. The agent may move within the centre third of the viewport without the camera/orbit-target moving. The camera only updates when the agent reaches the boundary of that centre third, reducing camera jitter.

- **2D**: dead zone on `camera_offset` (screen-space check against world-to-screen projection)
- **3D**: dead zone on `orbit_target` (check projected screen position of agent, only move target if agent exits centre-third of screen)

## Acceptance

- In 2D with follow on, selected agent can drift within the centre third without camera pan.
- When the agent crosses the centre-third boundary, camera pans to keep the agent inside the centre third.
- Same dead-zone behaviour applies in 3D mode with orbit_target.
- Camera does not jitter or jump when agent oscillates around the dead-zone boundary.
- Existing tests updated/extended to assert dead-zone behaviour.