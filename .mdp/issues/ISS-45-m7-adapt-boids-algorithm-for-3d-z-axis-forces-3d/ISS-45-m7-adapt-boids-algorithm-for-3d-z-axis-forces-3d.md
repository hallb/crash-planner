---
id: ISS-45
title: "M7: Adapt Boids algorithm for 3D (z-axis forces, 3D neighbourhood search)"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:36:10.030Z
updatedAt: 2026-03-09T01:36:10.030Z
---

## Description

Extend BoidsAlgorithm to operate in 3D when SimulationState has N×3 positions/velocities. Use 3D cKDTree for neighbour search. Apply separation, alignment, cohesion forces along z-axis. Constrain pitch to zero in 2D mode so existing 2D behaviour is unchanged. Update speed clamping to use 3D norm.
