---
id: M-10
title: 3D camera controls
status: Planning
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: "2026-03-08T00:00:00.000Z"
updatedAt: "2026-03-08T00:00:00.000Z"
---

#### Milestone Identity

**Milestone ID**: M-10
**Milestone Name**: 3D camera controls
**FR Mapping**:
- FR-001 (3D viewport navigation — orbit/zoom as part of real-time 3D view)

#### Goal

The user can orbit, pan, and zoom the 3D viewport using mouse controls when the simulation is in 3D mode.

#### Dependencies

M-7 3D mode

#### Plan

1. Implement orbit camera: mouse drag rotates yaw/pitch around flock centroid
2. Implement scroll-wheel zoom
3. Store camera state in ViewState; activate controls only when dimensions=3
4. Keep 2D pan/zoom behaviour unchanged
5. Add tests for camera state transitions

#### Outcome

- Orbit camera active in 3D mode (yaw/pitch around centroid)
- Scroll-wheel zoom in 3D mode
- 2D mode unaffected

#### Automated Verification (AI Gate)

1. Run full test suite

**Expected**:
- All tests pass
- No regressions in 2D mode or existing 3D behaviour

#### Human Verification (Human Gate)

1. Verify orbit, pan, and zoom feel natural in 3D mode
2. Confirm 2D mode controls are unaffected

#### Success Criteria

✅ Mouse drag orbits (yaw/pitch) around flock centroid in 3D mode
✅ Scroll wheel zooms in 3D mode
✅ 2D controls unchanged
✅ Tests pass
