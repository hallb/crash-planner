---
id: ISS-76
title: Telemetry shows 2D position/velocity when switched to 3D with agent selected
type: bug
status: Backlog
priority: Medium
labels: []
assignee: null
milestone: null
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-09T17:42:40.742Z
    author: cli
    body: "Bug reported: Telemetry persists after 2D→3D switch; shows 2D position/velocity; selected agent highlight may be lost"
createdAt: 2026-03-09T17:42:34.459Z
updatedAt: 2026-03-09T17:42:40.742Z
---

## Origin
- **Found during**: M-6 Flock2 + algorithm switching
- **Related issue**: ISS-40 (algorithm selector UI)

## Target Milestone
Unscheduled

## Description
**Observed**: When an agent is selected and Telemetry is shown, then the user switches from 2D to 3D dimensions:
- Telemetry continues to report (presumably about the selected agent)
- The selected agent is no longer highlighted in the 3D view
- Position and velocity are displayed in 2D format (x, y only), not 3D (x, y, z)

**Expected**: After switching to 3D, either:
- Selection is cleared and telemetry hidden (clean reset), or
- Selection persists and telemetry shows full 3D position/velocity (x, y, z)

## Steps to Reproduce
1. Start app in 2D mode
2. Select an agent (e.g. via click or Agent ID)
3. Expand Telemetry panel — verify 2D position and velocity shown
4. Switch to 3D via Controls → Dimensions → 3D
5. Observe: Telemetry still visible; position/velocity still in 2D format; agent may not be visually highlighted

## Environment
- 2D → 3D dimension switch
- Agent selection active (FR-010)
