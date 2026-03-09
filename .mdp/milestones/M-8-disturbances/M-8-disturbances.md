---
id: M-8
title: Disturbances
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

**Milestone ID**: M-8
**Milestone Name**: Disturbances
**FR Mapping**:
- FR-014 Fixed obstacles
- FR-015 Moving obstacles
- FR-016 Sudden noise
- FR-018 Obstacle config (fixed)
- FR-019 Obstacle config (moving)
- FR-020 Flock reaction and recovery

#### Goal

The user can define fixed obstacles (location, polygon) and moving obstacles (polygon, path) in config. The user can trigger sudden noise at runtime. The flock reacts to disturbances and recovers. All disturbance types work for both Boids and Flock2.

#### Dependencies

M-6 Flock2 + algorithm switching

#### Plan

1. Implement fixed obstacle support (location, polygon in config)
2. Implement moving obstacle support (polygon, path in config)
3. Implement sudden noise trigger at runtime
4. Add flock reaction logic (avoidance, evasion)
5. Add flock recovery behaviour
6. Ensure disturbances work for Boids and Flock2
7. Add tests for each disturbance type

#### Outcome

- Fixed obstacles configurable and rendered
- Moving obstacles configurable and rendered
- Sudden noise trigger works
- Flock reacts and recovers from all disturbance types
- Works for both Boids and Flock2

#### Automated Verification (AI Gate)

1. Run tests for fixed obstacles
2. Run tests for moving obstacles
3. Run tests for sudden noise
4. Run tests for flock reaction and recovery
5. Run full test suite

**Expected**:
- All tests pass
- Flock avoids obstacles and recovers

#### Human Verification (Human Gate)

1. Verify fixed obstacles block and deflect flock correctly
2. Verify moving obstacles affect flock as expected
3. Verify sudden noise causes visible flock reaction
4. Verify flock recovers after disturbance
5. Test with both Boids and Flock2

#### Success Criteria

✅ Fixed obstacles configurable and working
✅ Moving obstacles configurable and working
✅ Sudden noise trigger works
✅ Flock reacts and recovers
✅ All disturbance types work for Boids and Flock2
✅ Tests pass
