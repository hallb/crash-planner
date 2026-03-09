---
id: ISS-75
title: Click-to-select does not work in 3D mode
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-5
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T13:24:49.579Z
updatedAt: 2026-03-09T20:08:05.275Z
---

## Description

Click-to-select does not work in 3D mode. The implementation explicitly disables click handling when `state.dimensions == 3` ([renderer_2d.py](src/crash/renderer/renderer_2d.py) ~line 470). ID entry works in both modes.

## Triage

- **If selection was intended for 3D**: Treat as bug (FR-010 does not scope selection to 2D). Re-type as bug and prioritize.
- **If 3D click was out of scope for M-4**: Treat as enhancement. Implement screen-to-world ray casting (or project agents to screen and pick nearest) for 3D viewport.

## Related

- FR-010 (agent selection)
- ISS-26 (click and ID selection)
- FR-027 (2D/3D toggle)
