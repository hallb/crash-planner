---
id: M-6
title: Flock2 + algorithm switching
status: Completed
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: 2026-03-07T00:00:00.000Z
updatedAt: 2026-03-09T18:00:50.274Z
---

#### Milestone Identity

**Milestone ID**: M-6
**Milestone Name**: Flock2 + algorithm switching
**FR Mapping**:
- FR-004 Flock2 algorithm
- FR-006 Algorithm switching
- FR-007 Algorithm extensibility

#### Goal

The user selects between Boids and Flock2 via the UI. Flock2 implementation uses orientation-based model with topological neighbourhood, working in both 2D (angle-only, pitch=0) and 3D (quaternion orientation) modes. All existing features work with both algorithms in both dimensions. Algorithm extensibility interface is in place.

#### Dependencies

M-2 Parameter tuning + perf stats
M-7 3D mode

#### Plan

1. Implement Flock2 algorithm with orientation-based model and topological neighbourhood
2. Add algorithm extensibility interface (protocol/abstract base)
3. Add UI control to switch between Boids and Flock2
4. Ensure parameter tuning and all other existing features work with both algorithms
5. Add tests for Flock2 behaviour and algorithm switching

#### Outcome

- Flock2 algorithm implemented with orientation and topological neighbourhood
- Algorithm extensibility interface in place
- UI switch between Boids and Flock2
- All existing features work with both algorithms

#### Automated Verification (AI Gate)

1. Run unit tests for Flock2 algorithm
2. Run integration tests for algorithm switching
3. Verify both algorithms produce valid flock behaviour
4. Run full test suite

**Expected**:
- All tests pass
- No regressions in Boids or existing features

#### Human Verification (Human Gate)

1. Verify Flock2 flock behaviour looks correct (orientation-based, topological)
2. Confirm algorithm switch works smoothly
3. Verify all existing features work with both algorithms

#### Success Criteria

✅ Flock2 algorithm implemented — orientation-based, topological neighbourhood
✅ Flock2 works in both 2D mode (angle-only) and 3D mode (quaternion)
✅ Algorithm extensibility interface in place
✅ UI switch between Boids and Flock2
✅ All existing features work with both algorithms in both dimensions
✅ Tests cover both 2D and 3D Flock2 paths; mutation gate passes
