---
id: M-7
title: 3D mode
status: Completed
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: 2026-03-07T00:00:00.000Z
updatedAt: 2026-03-09T02:56:22.927Z
---

#### Milestone Identity

**Milestone ID**: M-7
**Milestone Name**: 3D mode
**FR Mapping**:
- FR-027 3D rendering
- FR-001 (complete) Murmuration visualization

#### Goal

The user toggles between 2D and 3D via the UI or config. Boids works in 3D; the protocol supports any algorithm in 3D. Switching dimensionality resets the simulation.

#### Dependencies

M-2 Parameter tuning + perf stats

#### Plan

1. Add 3D rendering pipeline (ModernGL/OpenGL)
2. Adapt Boids algorithm for 3D (z-axis, 3D neighbourhood)
3. Add UI/config toggle for 2D vs 3D
4. Reset simulation when switching dimensionality
5. Add 3D-specific tests

#### Outcome

- 3D rendering pipeline (perspective projection)
- Boids works in 3D
- 2D/3D toggle in UI and config
- Simulation resets on dimensionality change

#### Automated Verification (AI Gate)

1. Run tests for 3D rendering
2. Run tests for 2D/3D toggle
3. Verify Boids works in 3D
4. Run full test suite

**Expected**:
- All tests pass
- No regressions in 2D mode

#### Human Verification (Human Gate)

1. Verify 3D rendering looks correct in perspective
2. Verify dimensionality switch resets simulation correctly

#### Success Criteria

✅ 3D rendering pipeline active when dimensions=3
✅ Boids works in 3D
✅ 2D/3D toggle in UI and config
✅ Simulation resets on dimensionality change
✅ Tests pass
