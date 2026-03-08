---
id: M-2
title: Parameter tuning + perf stats
status: Planning
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: "2026-03-07T00:00:00.000Z"
updatedAt: "2026-03-07T00:00:00.000Z"
---

#### Milestone Identity

**Milestone ID**: M-2
**Milestone Name**: Parameter tuning + perf stats
**FR Mapping**:
- FR-002
- FR-003
- FR-025

**NFR Mapping**: NFR-003, NFR-007, NFR-009, NFR-012

#### Goal

The user adjusts Boids parameters (agent count, world size, neighbour radius, max speed, separation/alignment/cohesion weights) live and sees behaviour change. Live FPS, step time, and agent count display visible.

#### Dependencies

M-1 (MVP Boids 2D)

#### Plan

1. Add ImGui controls for Boids parameters (agent count, world size, neighbour radius, max speed, separation/alignment/cohesion weights)
2. Wire controls to simulation state for live updates
3. Add performance stats overlay (FPS, step time, agent count)
4. Ensure parameter changes take effect immediately without restart
5. Add tests for parameter application

#### Outcome

- Live parameter tuning via ImGui
- Performance stats (FPS, step time, agent count) visible
- Behaviour changes visible when parameters change

#### Automated Verification (AI Gate)

1. Run test suite
2. Verify parameter controls exist and are wired
3. Verify performance stats are displayed

**Expected**:
- All tests pass
- Parameter controls functional
- Stats overlay present

#### Human Verification (Human Gate)

1. Adjust each parameter and confirm flock behaviour changes
2. Verify FPS, step time, and agent count display are accurate
3. Confirm live updates work without restart
4. Set agent count to 10 and confirm agents are clearly visible and simulation runs without freeze (NFR-012, NFR-009)
5. Set agent count to 500 and confirm flock shape is perceptible, UI remains responsive, and no hard freeze occurs (NFR-003, NFR-007, NFR-009, NFR-012)

#### Success Criteria

✅ Live parameter controls for agent count, world size, neighbour radius, max speed, weights
✅ Behaviour changes visible on parameter change
✅ FPS, step time, agent count display visible
✅ No restart required for parameter updates
