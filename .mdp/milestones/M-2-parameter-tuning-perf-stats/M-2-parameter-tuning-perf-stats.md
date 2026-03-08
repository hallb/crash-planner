---
id: M-2
title: Parameter tuning + perf stats
status: Completed
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: 2026-03-07T00:00:00.000Z
updatedAt: 2026-03-08T19:39:23.510Z
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

#### M-2 Closeout Evidence (2026-03-08)

##### AI Gate Results

- `./script/test`: PASS (63 passed)
- `./script/cibuild`: PASS (ruff + format + mypy + tests + pip-audit)
- Startup smoke test (`timeout 8s ./script/server`): PASS (expected timeout exit after successful startup)

##### Mutation Testing Check

- Ran scoped mutation testing:
  - `./script/mutate --scope src/crash/data/config.py src/crash/simulation/engine.py src/crash/simulation/boids.py`
- Result observed: 239 killed, 2 survived.
- Survivors are tracked in `ISS-14` backlog per policy.

##### Human Gate Summary

- Parameter controls and metrics display verified in manual runs.
- Agent-count boundary checks verified by user:
  - 10 agents: clearly visible and stable
  - 500 agents: flock remains perceptible; UI remains responsive
- Final resize/controls bug regression verified fixed by user after display-size and resize handling correction.

##### NFR Acceptance Audit (M-2 mapping)

- **NFR-003 (agent range 10..500):** Satisfied (manual verification at 10 and 500)
- **NFR-007 (UI responsiveness):** Satisfied (controls responsive under normal/high load in final verification)
- **NFR-009 (graceful degradation):** Satisfied (no hard freeze in final manual checks)
- **NFR-012 (visual clarity at scale):** Satisfied (10-agent clarity and 500-agent perceptibility confirmed)

##### Deferred/Out-of-Scope at M-2 closeout

- `ISS-7` moved out of M-2 as deferred follow-up backlog work.
- `ISS-16` and `ISS-17` remain backlog by design.
