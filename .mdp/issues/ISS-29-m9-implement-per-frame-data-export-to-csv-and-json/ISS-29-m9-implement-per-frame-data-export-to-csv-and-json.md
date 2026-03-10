---
id: ISS-29
title: "M9: Implement per-frame data export to CSV and JSON"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy: [ISS-81]
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T22:55:54.253Z
updatedAt: 2026-03-10T01:00:00.000Z
---

## Description

Export per-frame agent positions and velocities to CSV and JSON for offline analysis (FR-024). Depends on the `[export]` config section added in ISS-81.

**CSV format:** One row per agent per frame.
- 2D: columns `tick, agent_id, x, y, vx, vy`
- 3D: columns `tick, agent_id, x, y, z, vx, vy, vz`

**JSON format:** Array of frames; each frame is an array of agent objects `{id, tick, position: [x,y[,z]], velocity: [vx,vy[,vz]]}`.

**In scope:**
- Implement `src/crash/data/export.py` with `write_csv(frames, path)` and `write_json(frames, path)` functions
- Collect frame snapshots from `SimulationState` (positions, velocities, tick) into a serialisable structure
- Respect `ExportConfig.data_formats` to write only the requested formats
- Write to `ExportConfig.output_dir`

**Acceptance:**
- CSV and JSON produced for a 2D sim contain correct columns/fields
- CSV and JSON produced for a 3D sim include the `z` / `vz` columns/fields
- Files are machine-readable; format is documented
- Unit tests: write to temp dir, assert schema and row count; tests cover both 2D and 3D state
