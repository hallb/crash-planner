---
id: ISS-42
title: "M6: Add tests for Flock2 algorithm and algorithm switching"
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
createdAt: 2026-03-09T01:35:52.669Z
updatedAt: 2026-03-09T15:50:48.254Z
---

## Description

Unit and integration tests for Flock2 and algorithm switching.

### Flock2 unit tests
- Topological neighbourhood selection: k-nearest returned, field-of-view filter applied, sorted for determinism
- Orientation update: thrust/drag mechanics advance velocity correctly, peripheral boundary term steers toward centroid when isolated
- **2D mode:** orientation stored as N×1 angles; pitch-constrained path produces valid positions/velocities
- **3D mode:** orientation stored as N×4 quaternions; yaw/pitch wrapping handled correctly; positions/velocities valid
- Edge cases: 0 agents (no crash), 1 agent, 500 agents (performance gate ≤10 ms at 100 agents per NFR-002)

### Algorithm switching integration tests
- Switching from Boids → Flock2 resets simulation state (new positions, re-seeded)
- Switching from Flock2 → Boids restores Boids behaviour; prior Boids tests remain green
- `orientations` array is `None` when Boids is active, populated when Flock2 is active
- Both algorithms work in both 2D and 3D modes (dimensionality × algorithm matrix)

### Acceptance criteria
- All new tests pass alongside existing 115 tests (no regressions)
- Mutation gate passes for `src/crash/simulation/flock2.py`, `src/crash/simulation/protocols.py`, and any new registry/engine files — survivors killed or documented as equivalent
