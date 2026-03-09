---
id: ISS-46
title: "M7: Add 3D rendering pipeline (perspective projection, z-component in vertex data)"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-50
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:36:10.081Z
updatedAt: 2026-03-09T01:40:36.937Z
---

## Description

Replace orthographic projection with perspective projection when dimensions=3. Upload z-component of agent positions to GPU vertex buffer. Update vertex shader to accept and use z-coordinate. Keep orthographic path for 2D mode. No new agent geometry needed — instanced draw continues.
