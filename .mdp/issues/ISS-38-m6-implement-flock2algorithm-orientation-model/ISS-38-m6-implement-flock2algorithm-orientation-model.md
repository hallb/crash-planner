---
id: ISS-38
title: "M6: Implement Flock2Algorithm (orientation model, topological neighbourhood)"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-6
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:35:39.404Z
updatedAt: 2026-03-09T01:35:39.404Z
---

## Description

Implement Flock2Algorithm implementing FlockingAlgorithm protocol. Use orientation-based steering model per Hoetzlein 2024: k-nearest topological neighbourhood via cKDTree, field-of-view angular filter, thrust/drag velocity update, peripheral boundary term for globular shape. Store orientations (N×1 angles in 2D) in SimulationState.
