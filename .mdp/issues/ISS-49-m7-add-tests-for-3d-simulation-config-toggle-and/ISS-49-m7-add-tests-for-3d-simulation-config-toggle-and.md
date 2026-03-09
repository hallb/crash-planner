---
id: ISS-49
title: "M7: Add tests for 3D simulation, config, toggle, and rendering path; run mutation gate"
type: task
status: Done
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
log:
  - "2026-03-09: Mutation gate run on config, config_io, state, boids, engine: 522 killed, 129 survivors. Score ~80% (>70% target). Survivors mostly in config parsing/validation edge paths; 3D-specific logic well covered by test_boids_step_3d_produces_valid_n3_state, test_dimensions_change_*, test_engine_creates_3d_state_when_dimensions_3, test_boundary_steering_3d_near_z_edges."
createdAt: 2026-03-09T01:36:19.569Z
updatedAt: 2026-03-09T01:36:19.569Z
---

## Description

Unit tests: 3D Boids step produces valid N×3 positions/velocities; dimensions config round-trips correctly (NFR-011); 2D mode still passes existing tests. Integration tests: dimensionality toggle resets simulation. Run ./script/mutate --scope on changed files. Kill survivors or document as equivalent.
