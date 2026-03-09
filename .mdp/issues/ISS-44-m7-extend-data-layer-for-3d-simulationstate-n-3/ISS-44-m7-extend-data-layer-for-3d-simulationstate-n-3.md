---
id: ISS-44
title: "M7: Extend data layer for 3D (SimulationState N×3 arrays, world_bounds depth, dimensions config)"
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
createdAt: 2026-03-09T01:36:09.977Z
updatedAt: 2026-03-09T01:36:09.977Z
---

## Description

Extend SimulationState so positions and velocities support N×2 or N×3 arrays. Add optional depth to world_bounds. Add dimensions field (int, default 2, valid: 2 or 3) to GlobalParams and TOML [global] config section. Update config save/load and validation. z=0 in 2D mode keeps backward compatibility.

Per FR-027 (dimensionality configurable in [global] config section, per FR-021) and FR-001 (simulation state must support N×3 positions/velocities for 3D rendering). New dimensions field must round-trip correctly per NFR-011.
