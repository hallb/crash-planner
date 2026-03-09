---
id: ISS-74
title: Highlight neighbours in telemetry with distinct colour
type: task
status: Backlog
priority: null
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
log: []
createdAt: 2026-03-09T13:20:48.065Z
updatedAt: 2026-03-09T13:20:48.065Z
---

## Description

When an agent is selected, the telemetry panel shows Neighbours count. Add an affordance (checkbox/toggle) "Highlight neighbours" that, when enabled, renders those neighbour agents in a distinct colour (e.g. cyan or green) so the user can visually identify which agents are counted as neighbours.

## Related

- ISS-27 (telemetry panel)
- FR-010 (selection/telemetry)

## Technical notes

- Neighbour set is already computed in controls for the count; the same logic can be reused.
- ViewState would need a `highlight_neighbours: bool` (or similar).
- Renderer would draw neighbour agents in a second pass when enabled.
