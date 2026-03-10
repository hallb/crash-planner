---
id: ISS-33
title: "M9: Add export tests, performance checks, and mutation gate"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy: [ISS-29, ISS-30, ISS-31, ISS-82]
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T22:55:54.673Z
updatedAt: 2026-03-10T01:00:00.000Z
---

## Description

Verify export correctness, NFR-008 performance thresholds, 2D/3D coverage, and mutation quality gate for all M-9 export code.

**In scope:**

### Format correctness
- CSV: assert correct column headers for 2D (`tick,agent_id,x,y,vx,vy`) and 3D (`tick,agent_id,x,y,z,vx,vy,vz`)
- JSON: assert correct schema for 2D and 3D agent objects
- GIF: assert valid GIF header and correct frame count given a known frame interval
- MP4: assert ffmpeg subprocess called with correct args (mocked)

### Performance (NFR-008)
- **Data export:** benchmark write of 100 agents × 10 min at 60 fps = 36,000 frames; assert completion ≤ 30 s
- **Video export:** assert encoding throughput ≥ 0.5× real-time (stub or real ffmpeg); document WSL2 limits if 2× target is unachievable
- Both benchmarks implemented as pytest-benchmark tests scoped to export functions

### 2D and 3D coverage
- All format tests run against both a 2D `SimulationState` fixture and a 3D fixture

### Mutation gate
- Run `./script/mutate --scope src/crash/data/export.py`
- Kill survivors or document as equivalent mutants

**Acceptance:**
- All format tests pass
- NFR-008 benchmarks pass or limits documented
- Mutation gate complete
