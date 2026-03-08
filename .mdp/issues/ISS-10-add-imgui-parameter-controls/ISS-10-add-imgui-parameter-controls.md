---
id: ISS-10
title: Add ImGui parameter controls for Boids
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-2
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-8
  - ISS-9
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T02:05:00.000Z
updatedAt: 2026-03-08T19:01:55.661Z
---

## Description

ImGui sliders for agent_count (10–500), world_bounds (width, height), visual_range, protected_range, max_speed, min_speed, turn_factor, separation_weight, alignment_weight, cohesion_weight. Wire to Configuration. Invalid values produce error per NFR-005. FR-002, FR-003.
