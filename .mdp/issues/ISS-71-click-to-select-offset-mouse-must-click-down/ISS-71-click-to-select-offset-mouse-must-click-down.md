---
id: ISS-71
title: "Click-to-select offset: mouse must click down-right of target bird"
type: bug
status: Backlog
priority: High
labels: []
assignee: null
milestone: M-4
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-09T12:57:10.347Z
    author: cli
    body: "Bug reported during M-4 Human Gate: click offset down-right of target; hypothesis: metrics bar or viewport mapping"
createdAt: 2026-03-09T12:56:55.389Z
updatedAt: 2026-03-09T12:57:10.347Z
---

## Origin

- **Found during**: M-4 Flock metrics + agent selection
- **Related issue**: ISS-26 (agent selection via click and ID input)

## Target Milestone

M-4 (fix ASAP — blocks Human Gate approval)

## Description

**Observed**: To select an agent by clicking, the user must click at an offset down and to the right of the target bird. Clicking directly on the bird often fails to select it.

**Expected**: Clicking on or near the visible bird should select it.

**Hypothesis**: May be related to metrics bar height or arena viewport calculation (screen-to-world mapping). The metrics bar adds vertical offset; if coordinate mapping does not account for layout correctly, clicks would appear offset.

## Steps to Reproduce

1. Start the app in 2D mode.
2. Hover over a bird and click directly on it.
3. Observe: selection often misses; clicking down-right of the bird selects it.
4. Repeat with different birds and positions.

## Environment

- 2D mode
- Default agent count and world size
- Metrics bar visible (46px height)
