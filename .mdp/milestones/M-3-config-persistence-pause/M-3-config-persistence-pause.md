---
id: M-3
title: Config persistence + pause
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

**Milestone ID**: M-3
**Milestone Name**: Config persistence + pause
**FR Mapping**:
- FR-008
- FR-021

**NFR Mapping**: NFR-005, NFR-010, NFR-011

#### Goal

The user can save parameters to a TOML config file (global + boids sections), load them back, pause and resume the simulation, and get reproducible results with the same seed.

#### Dependencies

M-2 (Parameter tuning + perf stats)

#### Plan

1. Define TOML config schema (global + boids sections)
2. Implement save/load for config files
3. Add pause/resume controls to simulation loop
4. Add seed support for reproducible runs
5. Wire config load to parameter initialization
6. Add tests for config persistence and determinism

#### Outcome

- TOML config save/load works
- Pause/resume functional
- Same seed produces same results
- Config schema documented

#### Automated Verification (AI Gate)

1. Run test suite
2. Test save config, load config, verify parameters match
3. Test pause/resume state
4. Test deterministic run with fixed seed

**Expected**:
- All tests pass
- Config round-trip preserves parameters
- Pause/resume works
- Same seed yields same simulation output

#### Human Verification (Human Gate)

1. Save config, modify params, load config — verify restoration
2. Pause and resume — verify simulation state preserved
3. Run twice with same seed — verify identical behaviour

#### Success Criteria

✅ TOML config save/load (global + boids sections)
✅ Pause and resume simulation
✅ Reproducible runs with same seed
✅ Config schema documented
