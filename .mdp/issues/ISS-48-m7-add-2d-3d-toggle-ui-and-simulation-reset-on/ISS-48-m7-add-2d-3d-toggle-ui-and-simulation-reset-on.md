---
id: ISS-48
title: "M7: Add 2D/3D toggle UI and simulation reset on dimensionality change"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-50
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:36:19.516Z
updatedAt: 2026-03-09T01:40:37.110Z
---

## Description

Add a 2D/3D selector (dropdown or toggle) to the ImGui controls panel. When switched, reset and restart the simulation with current parameters in the new dimensionality. Update the UI to show/hide 3D-specific controls (camera, depth) accordingly. Indicate selected mode clearly per FR-027.

### Notes from ISS-50 spike

- No impact on ImGui overlay: pyimgui composes correctly over 3D viewport. Toggle UI can be a standard ImGui control.
