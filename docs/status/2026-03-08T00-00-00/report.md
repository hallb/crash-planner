# Project Status Report

**Generated:** 2026-03-08T00:00:00+00:00

---

## Health snapshot

| | Count |
|---|---|
| Milestones completed | 4 |
| Milestones in progress | 0 |
| Milestones planned | 6 |
| Issues done | 25 |
| Issues in progress | 0 |
| Issues open (backlog) | 18 |
| Bugs open | 1 |
| Bugs resolved | 1 |

---

## Milestone roadmap

```mermaid
flowchart TD
  classDef done fill:#4caf50,color:#fff,stroke:#388e3c
  classDef active fill:#ff9800,color:#fff,stroke:#e65100
  classDef planned fill:#9e9e9e,color:#fff,stroke:#616161

  M1["M-1: MVP Boids 2D"]:::done
  M2["M-2: Parameter tuning + perf stats"]:::done
  M3["M-3: Config persistence + pause"]:::done
  M4["M-4: Flock metrics + agent selection"]:::planned
  M5["M-5: Agent follow + trajectory trail"]:::planned
  M6["M-6: Flock2 algorithm switching"]:::planned
  M7["M-7: 3D mode"]:::done
  M8["M-8: Disturbances"]:::planned
  M9["M-9: Export"]:::planned
  M10["M-10: 3D camera controls"]:::planned

  M1 --> M2
  M2 --> M3
  M2 --> M4
  M2 --> M6
  M2 --> M7
  M3 --> M9
  M4 --> M5
  M6 --> M8
  M7 --> M10
```

---

## Per-milestone summary

| Milestone | Status | Issues Done / Total | Bugs Raised | Bugs Resolved |
|-----------|--------|---------------------|-------------|---------------|
| M-1: MVP Boids 2D | Done | 6 / 6 | 0 | 0 |
| M-2: Parameter tuning + perf stats | Completed | 7 / 7 | 1 | 1 |
| M-3: Config persistence + pause | Completed | 6 / 6 | 0 | 0 |
| M-4: Flock metrics + agent selection | Planning | 0 / 6 | 1 | 0 |
| M-5: Agent follow + trajectory trail | Planning | 0 / 0 | 0 | 0 |
| M-6: Flock2 algorithm switching | Planning | 0 / 7 | 0 | 0 |
| M-7: 3D mode | Completed | 6 / 6 | 0 | 0 |
| M-8: Disturbances | Planning | 0 / 0 | 0 | 0 |
| M-9: Export | Planning | 0 / 5 | 0 | 0 |
| M-10: 3D camera controls | Planning | 0 / 1 | 0 | 0 |

---

## Currently in-flight

No issues currently in progress.

---

## Open bugs by priority

| ID | Title | Priority | Milestone |
|----|-------|----------|-----------|
| ISS-7 | Birds disappear at viewport edge (visualization) | Medium | M-4 |

---

## Unassigned backlog

| ID | Title | Type | Priority |
|----|-------|------|----------|
| ISS-14 | Document surviving boids mutation test mutants | chore | Low |
| ISS-16 | Window resize support and world boundary behavior | feature | Medium |
| ISS-17 | Improve parameter controls with direct input, help text, and reset | feature | Low |
| ISS-34 | Support named config files for multiple saved configurations | feature | null |
| ISS-35 | Codify pull-before-update and commit-on-status-change in execute-milestone skill | chore | null |
| ISS-36 | Generate milestone/issue status reports with Mermaid Gantt charts | feature | null |
| ISS-51 | Enhance 3D visual depth cues (richer bird geometry, bounding box, size attenuation) | feature | null |
