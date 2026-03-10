---
id: ISS-80
title: Viewport follow does not work in 3D mode
type: bug
status: Backlog
priority: Medium
labels: []
assignee: null
milestone: M-10
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: [ISS-58]
checklist: []
log:
  - timestamp: "2026-03-09T22:00:00.000Z"
    author: human-gate
    body: "Human Gate (M-5): Follow toggle works in 2D only; does not work at all in 3D."
createdAt: "2026-03-09T22:00:00.000Z"
updatedAt: "2026-03-09T22:00:00.000Z"
---

## Origin

- **Found during**: M-5 Human Gate (viewport follow verification)
- **Related**: ISS-58 (viewport follow), M-10 (3D camera controls)

## Description

**Observed**: With follow enabled and simulation in 3D mode, the viewport/camera does not follow the selected agent. Follow behaviour is 2D-only.

**Expected**: When follow is on in 3D mode, the orbit camera (or equivalent 3D view) should track the selected agent so the agent remains in view (e.g. kept in centre or centre-third of the 3D viewport).

**Scope**: Implement or fix viewport follow for 3D mode; likely integrates with orbit camera state (yaw/pitch/distance) in M-10.

## Acceptance

- In 3D mode with follow on and an agent selected, the 3D camera tracks the selected agent (e.g. orbit target follows agent position).
- Toggle follow off/on behaves correctly in 3D.
- No regression in 2D follow behaviour.
