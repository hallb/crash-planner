---
id: M-4
title: Flock metrics + agent selection
status: Completed
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: 2026-03-07T00:00:00.000Z
updatedAt: 2026-03-09T13:23:15.763Z
---

#### Milestone Identity

**Milestone ID**: M-4
**Milestone Name**: Flock metrics + agent selection
**FR Mapping**:
- FR-009
- FR-010
- FR-011

#### Goal

The user reads live flock metrics (average speed, flock density, cohesion radius, alignment index), clicks or enters an ID to select an agent, sees it highlighted with a distinct colour, and views its telemetry (position, velocity, neighbour count).

#### Dependencies

M-2 (Parameter tuning + perf stats)

#### Plan

1. Compute and display flock metrics (average speed, flock density, cohesion radius, alignment index)
2. Add click-to-select for agents (map screen coords to agent ID)
3. Add ID entry field for agent selection
4. Render selected agent with distinct highlight colour
5. Display selected agent telemetry (position, velocity, neighbour count)
6. Add tests for metric computation and selection logic

#### Outcome

- Live flock metrics displayed
- Agent selection via click or ID entry
- Selected agent highlighted
- Telemetry panel for selected agent

#### Automated Verification (AI Gate)

1. Run test suite
2. Test metric computation functions
3. Test selection mapping (coords to ID)

**Expected**:
- All tests pass
- Metrics computed correctly
- Selection logic works

#### Human Verification (Human Gate)

1. Verify flock metrics update in real time and look plausible
2. Click an agent — verify highlight and telemetry
3. Enter agent ID — verify selection works
4. Confirm telemetry (position, velocity, neighbour count) is accurate

#### Success Criteria

✅ Live flock metrics (average speed, density, cohesion radius, alignment index)
✅ Click or ID entry selects agent
✅ Selected agent highlighted with distinct colour
✅ Telemetry (position, velocity, neighbour count) displayed for selected agent
