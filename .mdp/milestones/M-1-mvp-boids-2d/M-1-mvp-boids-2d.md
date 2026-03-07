---
id: M-1
title: MVP Boids 2D
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

**Milestone ID**: M-1
**Milestone Name**: MVP Boids 2D
**FR Mapping**:
- FR-001 (partial: 2D only)
- FR-005

**NFR Mapping**: NFR-001, NFR-002, NFR-004, NFR-013, NFR-014, NFR-015, NFR-016

#### Goal

The user launches the app and sees an animated Boids murmuration in 2D. Hardcoded defaults (~100 agents, sensible Boids params). No UI controls, no config, no metrics.

#### Dependencies

None

#### Plan

1. Set up project structure per solution design (Python, Pygame, ModernGL, NumPy, SciPy)
2. Implement Boids algorithm core (separation, alignment, cohesion)
3. Create 2D rendering pipeline for agent positions
4. Add main loop with fixed timestep for simulation
5. Use hardcoded defaults (~100 agents, sensible Boids params)
6. Add automated tests per NFR-014
7. Ensure reproducible build per NFR-015 and static analysis per NFR-016

#### Outcome

- Boids simulation runs in 2D with ~100 agents
- User sees animated murmuration on launch
- No UI controls, config, or metrics
- Tests pass, build reproducible

#### Automated Verification (AI Gate)

1. Run test suite
2. Run build/package command
3. Run static analysis

**Expected**:
- All tests pass
- Build succeeds
- No static analysis errors

#### Human Verification (Human Gate)

1. Launch the app and confirm animated Boids murmuration is visible
2. Verify flock behaviour looks coherent (separation, alignment, cohesion)
3. Confirm no UI controls, config, or metrics are present

#### Success Criteria

✅ App launches and displays 2D Boids simulation
✅ ~100 agents with sensible default parameters
✅ Animated murmuration visible
✅ No UI controls, config, or metrics
✅ Tests pass, build reproducible
