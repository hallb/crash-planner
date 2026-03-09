---
id: ISS-42
title: "M6: Add tests for Flock2 algorithm and algorithm switching"
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
createdAt: 2026-03-09T01:35:52.669Z
updatedAt: 2026-03-09T01:35:52.669Z
---

## Description

Unit tests for Flock2 step computation: neighbourhood selection, orientation update, thrust/drag mechanics, boundary term. Integration tests for algorithm switching: engine resets on switch, Boids tests remain green, Flock2 produces valid positions/velocities. Cover happy path and edge cases (min agents, max agents).
