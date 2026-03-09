---
id: ISS-50
title: "M7: Spike — trial 3D rendering with Pygame/ModernGL/pyimgui"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:40:33.273Z
updatedAt: 2026-03-09T01:40:33.273Z
---

## Questions to answer

1. Does the existing Pygame/ModernGL window setup support depth buffering, or does OpenGL context creation need rework?
2. Can the current shader pipeline adapt to perspective projection and 3D vertex data, or does it need a rewrite?
3. Does the pyimgui overlay still compose correctly over a 3D viewport with depth testing enabled?
4. What does instanced 3D agent rendering look like — flat triangles in 3D space, or do we need real geometry?

## Deliverables

- Documented answers to the four questions above
- Findings recorded as notes on ISS-46 (rendering pipeline) and ISS-48 (toggle UI)
- Any code written during the spike is discarded — it is not committed or carried forward

## Definition of done

Findings documented; dependent issues unblocked.