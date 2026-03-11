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
- FR-001 (3D viewport navigation — orbit/pan/zoom as part of real-time 3D view)

#### Goal

The user can orbit, pan, and zoom the 3D viewport using mouse controls when the simulation is in 3D mode. Viewport follow works in 3D.

#### Dependencies

M-7 3D mode

#### Issue Sequence

ISS-52 (ViewState) → ISS-53 (orbit) / ISS-54 (zoom) / ISS-87 (pan) → ISS-55 (view matrix) → ISS-80 (3D follow) → ISS-56 (tests) → ISS-88 (mutation gate)

#### Plan

1. **ISS-52** — Extend ViewState with orbit camera state (yaw, pitch, distance, target)
2. **ISS-53** — Implement mouse-drag yaw/pitch orbit (3D mode only); depends on ISS-52
3. **ISS-54** — Implement scroll-wheel zoom in 3D mode; depends on ISS-52
4. **ISS-87** — Implement 3D pan (translate orbit target via middle-mouse or shift+drag); depends on ISS-52
5. **ISS-55** — Wire orbit state into renderer 3D view matrix; depends on ISS-52
6. **ISS-80** — Fix viewport follow in 3D mode (orbit target tracks selected agent); depends on ISS-52, ISS-55
7. **ISS-56** — Tests for camera state transitions and 2D mode regression; depends on ISS-52–55, ISS-87
8. **ISS-88** — Mutation gate scoped to camera controls and view-state code; depends on ISS-56

#### Removed from M-10 (review 2026-03-11)

- **ISS-47** — Cancelled; superseded by ISS-52–56 breakdown.
- **ISS-51** — Moved out; visual depth cue enhancements are orthogonal to camera controls.
- **ISS-79** — Moved out; 2D follow dead-zone bug is unrelated to 3D camera controls.

#### Outcome

- Orbit camera active in 3D mode (yaw/pitch around centroid or followed agent)
- Scroll-wheel zoom in 3D mode
- Pan translates orbit target laterally in 3D mode
- Viewport follow works in 3D mode (orbit target tracks selected agent)
- 2D mode unaffected
- Mutation gate passed

#### Automated Verification (AI Gate)

1. Run full test suite
2. Run mutation gate (`./script/mutate --scope` on touched files)

**Expected**:
- All tests pass
- No regressions in 2D mode or existing 3D behaviour
- No unjustified surviving mutants

#### Human Verification (Human Gate)

1. Verify orbit, pan, and zoom feel natural in 3D mode
2. Verify 3D follow tracks selected agent smoothly
3. Confirm 2D mode controls are unaffected

#### Success Criteria

✅ Mouse drag orbits (yaw/pitch) around flock centroid in 3D mode
✅ Middle-mouse/shift+drag pans (translates orbit target) in 3D mode
✅ Scroll wheel zooms in 3D mode
✅ 3D follow moves orbit target to track selected agent
✅ 2D controls unchanged
✅ Tests pass
✅ Mutation gate passed
