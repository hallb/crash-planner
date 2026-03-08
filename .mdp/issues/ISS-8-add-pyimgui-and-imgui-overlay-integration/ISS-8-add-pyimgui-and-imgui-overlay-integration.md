---
id: ISS-8
title: Add pyimgui and ImGui overlay integration
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-2
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T02:03:19.237Z
updatedAt: 2026-03-08T02:03:19.237Z
---

## Description

Add pyimgui to deps; integrate with Pygame+ModernGL render loop; render imgui frame each tick. Per 02-tech-stack, 04-front-end-design.

**Note (NFR-015):** Verify that pyimgui has no new system-level dependencies beyond what `script/bootstrap` already installs (`libgl-dev`, `libegl-dev`). If additional packages are required, update `script/bootstrap` accordingly.
