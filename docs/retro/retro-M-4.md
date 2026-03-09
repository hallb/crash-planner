# Retrospective: M-4 Flock metrics + agent selection

**Milestone:** M-4
**Status:** In progress

---

## Observations

_Capture observations here throughout the milestone. Promote actionable items to retro issues when ready._

### What worked well

- App starts OK.
- Metrics display works; values seem plausible.
- Select-by-ID works correctly.
- Telemetry (position, velocity, neighbour count) displays correctly when an agent is selected.
- Clear selection works correctly.

### Friction / what didn't work

- **Click-to-select offset**: Mouse must be clicked at an offset down and to the right of the target bird to select it. May be related to metrics bar height or arena viewport. Recorded as ISS-71 (High-priority bug, fix ASAP).
- Metrics lack explanatory text; users may not understand Speed, Density, Cohesion, Align. Recorded as ISS-72 for future improvement.
- When clicking to select an agent, the selected agent's ID is not populated in the Agent ID input field or displayed in the telemetry panel header. Recorded as ISS-73.

### Process observations

### Ideas for rules or skills

---

## Promoted items

Items from the observations above that became actionable issues.

| Issue | Observation | Status |
|-------|-------------|--------|
| ISS-71 | Click-to-select offset: mouse must click down-right of target bird (bug, fix ASAP) | Backlog |
| ISS-72 | Add explanatory text for flock metrics | Backlog |
| ISS-73 | Populate agent ID in selection field or telemetry when clicking | Backlog |
| ISS-74 | Highlight neighbours in telemetry with distinct colour (toggle in telemetry panel) | Backlog |
