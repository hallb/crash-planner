---
id: ISS-47
title: "M7: Implement 3D camera controls (orbit: yaw/pitch around centroid, scroll to zoom)"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: "null"
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-50
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:36:10.132Z
updatedAt: 2026-03-09T01:42:06.647Z
---

## Description

Implement orbit camera for 3D mode: mouse drag rotates yaw/pitch around flock centroid, scroll wheel zooms. Store camera state in ViewState. Camera controls are active only when dimensions=3; 2D pan/zoom behaviour unchanged. Fly mode is deferred.
