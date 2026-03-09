---
id: ISS-49
title: "M7: Add tests for 3D simulation, config, toggle, and rendering path; run mutation gate"
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
createdAt: 2026-03-09T01:36:19.569Z
updatedAt: 2026-03-09T01:36:19.569Z
---

## Description

Unit tests: 3D Boids step produces valid N×3 positions/velocities; dimensions config round-trips correctly (NFR-011); 2D mode still passes existing tests. Integration tests: dimensionality toggle resets simulation. Run ./script/mutate --scope on changed files. Kill survivors or document as equivalent.
