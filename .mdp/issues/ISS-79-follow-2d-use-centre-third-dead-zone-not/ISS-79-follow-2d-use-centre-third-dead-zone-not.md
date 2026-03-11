---
id: ISS-79
title: Follow (2D) — use centre-third dead zone; camera moves only when bird leaves it
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
updatedAt: 2026-03-11T18:19:21.377Z
---

## Origin

- **Found during**: M-5 Human Gate (viewport follow verification)
- **Related**: ISS-58 (viewport follow implementation)

## Description

**Current behaviour (2D)**: With follow enabled, the camera keeps the selected agent pinned to the centre of the viewport (so the bird is always centred).

**Intended behaviour**: The camera should use a **centre-third dead zone**. The selected agent may move within the centre third of the viewport without the camera moving; the camera only updates when the agent reaches the boundary of that centre third. This reduces constant camera movement and jitter.

**Scope**: 2D mode only. 3D follow is tracked in ISS-80.

## Acceptance

- In 2D with follow on, selected agent can drift within the centre third without camera pan.
- When the agent crosses the centre-third boundary, camera pans to keep the agent inside (or at the edge of) the centre third.
- Existing tests for follow offset updated or extended to assert dead-zone behaviour.
