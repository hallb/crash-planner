---
id: ISS-47
title: "Implement 3D camera controls (orbit: yaw/pitch around centroid, scroll to zoom)"
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
  - ISS-50
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-11T18:19:21.228Z
    author: M-10-review
    body: "Cancelled: superseded by ISS-52 through ISS-56, which break this issue into discrete tasks (ViewState extension, mouse orbit, scroll zoom, view matrix update, tests)."
createdAt: 2026-03-09T01:36:10.132Z
updatedAt: 2026-03-11T18:19:21.228Z
---

## Description

Implement orbit camera for 3D mode: mouse drag rotates yaw/pitch around flock centroid, scroll wheel zooms. Store camera state in ViewState. Camera controls are active only when dimensions=3; 2D pan/zoom behaviour unchanged. Fly mode is deferred.
