---
id: M-5
title: Agent follow + trajectory trail
status: Completed
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: 2026-03-07T00:00:00.000Z
updatedAt: 2026-03-09T23:59:06.026Z
---

#### Milestone Identity

**Milestone ID**: M-5
**Milestone Name**: Agent follow + trajectory trail
**FR Mapping**:
- FR-012
- FR-026

#### Goal

The user toggles viewport follow to lock the camera on the selected agent (kept in centre third of viewport) and sees a trail of recent positions rendered behind the selected agent; trail has bounded length and clears on deselect.

#### Dependencies

M-4 (Flock metrics + agent selection)

#### Plan

1. Add viewport follow toggle (camera locks to selected agent)
2. Keep selected agent in centre third of viewport when following
3. Store recent positions for selected agent (bounded buffer)
4. Render trail as line/polyline behind selected agent
5. Clear trail on deselect
6. Add tests for follow logic and trail rendering

#### Outcome

- Viewport follow toggle functional
- Selected agent kept in centre third when following
- Trail of recent positions visible
- Trail clears on deselect

#### Automated Verification (AI Gate)

1. Run test suite
2. Test follow mode keeps agent in centre third
3. Test trail buffer bounded and clears on deselect

**Expected**:
- All tests pass
- Follow logic correct
- Trail management works

#### Human Verification (Human Gate)

1. Toggle follow — verify camera tracks selected agent
2. Verify agent stays in centre third of viewport
3. Confirm trail renders behind agent with bounded length
4. Deselect — verify trail clears

#### Success Criteria

✅ Viewport follow toggle locks camera to selected agent
✅ Selected agent kept in centre third of viewport
✅ Trail of recent positions rendered behind agent
✅ Trail has bounded length, clears on deselect
