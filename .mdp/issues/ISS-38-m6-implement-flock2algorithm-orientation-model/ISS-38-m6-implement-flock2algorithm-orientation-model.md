---
id: ISS-38
title: "M6: Implement Flock2Algorithm — orientation model, topological neighbourhood, 2D and 3D modes"
type: task
status: Done
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
updatedAt: 2026-03-09T15:45:40.371Z
---

## Description

Implement Flock2Algorithm satisfying the FlockingAlgorithm protocol. Use the orientation-based steering model per Hoetzlein 2024: k-nearest topological neighbourhood via cKDTree, field-of-view angular filter, thrust/drag velocity update, peripheral boundary term for globular shape.

### Dimensionality requirements

**3D mode (primary path):** Orientation is a quaternion per agent (N×4 array stored in `SimulationState.orientations`). Yaw/pitch targets are computed from neighbour influence; quaternion integration advances orientation each tick. Velocity derives from orientation and thrust/drag. Note yaw wraps ±180° and pitch wraps ±90° — handle sphere wrapping correctly.

**2D mode (constrained path):** Pitch is fixed at zero. Orientation simplifies to a scalar angle per agent (N×1 array). Quaternion machinery is not needed; use angle arithmetic directly. This is a dimensionality branch on `state.dimensions`, not a separate algorithm.

Both modes must:
- Populate `SimulationState.orientations` (angles in 2D, quaternions in 3D)
- Produce valid `positions` and `velocities` after each step
- Respect world boundaries via the peripheral boundary term
- Pass the neighbour sort for determinism (NFR-010)

M-7 (3D mode) is already complete, so the 3D renderer pipeline is ready to consume `orientations`.
