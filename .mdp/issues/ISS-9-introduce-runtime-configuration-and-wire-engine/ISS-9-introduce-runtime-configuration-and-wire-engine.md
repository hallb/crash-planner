---
id: ISS-9
title: Introduce runtime Configuration; Engine reinitializes on agent_count and world_bounds change
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
createdAt: 2026-03-08T02:05:00.000Z
updatedAt: 2026-03-08T02:05:00.000Z
---

## Description

Create in-memory Configuration dataclass with Boids params, agent_count, world_bounds (per 06-data-design). Engine reads config each step; agent_count or world_bounds change triggers reinit (resize arrays, respawn agents). Per 07-interface-contracts: Controls writes to Configuration; Engine reads on each tick.
