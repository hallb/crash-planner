# Project Status Report

**Generated:** 2026-03-09T20:02:40.354920+00:00

---

## Health snapshot

| | Count |
|---|---|
| Milestones completed | 6 |
| Milestones in progress | 0 |
| Milestones planned | 4 |
| Issues done | 38 |
| Issues in progress | 0 |
| Issues open (backlog) | 29 |
| Bugs open | 2 |
| Bugs resolved | 2 |

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
  M4["M-4: Flock metrics + agent selection"]:::done
  M5["M-5: Agent follow + trajectory trail"]:::planned
  M6["M-6: Flock2 + algorithm switching"]:::done
  M7["M-7: 3D mode"]:::done
  M8["M-8: Disturbances"]:::planned
  M9["M-9: Export"]:::planned
  M10["M-10: 3D camera controls"]:::planned

  M1 --> M2
  M2 --> M3
  M2 --> M4
  M2 --> M7
  M4 --> M5
  M2 --> M6
  M7 --> M6
  M6 --> M8
  M3 --> M9
  M7 --> M10
```

---

## Per-milestone summary

| Milestone | Status | Issues Done / Total | Bugs Raised | Bugs Resolved |
|-----------|--------|---------------------|-------------|---------------|
| M-1: MVP Boids 2D | Completed | 6 / 6 | 0 | 0 |
| M-2: Parameter tuning + perf stats | Completed | 7 / 7 | 1 | 1 |
| M-3: Config persistence + pause | Completed | 6 / 6 | 0 | 0 |
| M-4: Flock metrics + agent selection | Completed | 6 / 6 | 1 | 1 |
| M-5: Agent follow + trajectory trail | Planning | 0 / 8 | 1 | 0 |
| M-6: Flock2 + algorithm switching | Completed | 7 / 7 | 0 | 0 |
| M-7: 3D mode | Completed | 6 / 6 | 0 | 0 |
| M-8: Disturbances | Planning | 0 / 8 | 0 | 0 |
| M-9: Export | Planning | 0 / 5 | 0 | 0 |
| M-10: 3D camera controls | Planning | 0 / 7 | 0 | 0 |

---

## Currently in-flight

No issues currently in progress.

---

## Open bugs by priority

| ID | Title | Priority | Milestone |
|----|-------|----------|-----------|
| ISS-7 | Birds disappear at viewport edge (visualization) | Medium | M-5 |
| ISS-76 | Telemetry shows 2D position/velocity when switched to 3D with agent selected | Medium | — |

---

## Unassigned backlog

| ID | Title | Type | Priority |
|----|-------|------|----------|
| ISS-14 | Document surviving boids mutation test mutants | chore | Low |
| ISS-17 | Improve parameter controls with direct input, help text, and reset | feature | Low |
| ISS-34 | Support named config files for multiple saved configurations | feature | — |
| ISS-72 | Add explanatory text for flock metrics | task | — |
| ISS-73 | Populate agent ID in selection field or telemetry when clicking | task | — |
| ISS-74 | Highlight neighbours in telemetry with distinct colour | task | — |
| ISS-75 | Click-to-select does not work in 3D mode | task | — |
| ISS-76 | Telemetry shows 2D position/velocity when switched to 3D with agent selected | bug | Medium |
