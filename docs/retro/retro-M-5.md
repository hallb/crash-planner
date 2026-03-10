# Retrospective: M-5 Agent follow + trajectory trail

**Milestone:** M-5
**Status:** Completed

---

## Observations

_Capture observations here throughout the milestone. Promote actionable items to retro issues when ready._

### What worked well

- Follow toggle (2D), bounded trail buffer, and clear-on-deselect implemented and covered by tests.
- **Trail**: Works; deselection clears trail as intended.
- ISS-7, ISS-75, ISS-76 (viewport edge, 3D click-to-select, telemetry 2D/3D) resolved during milestone.

### Friction / what didn't work

- **2D follow behaviour (Human Gate)**: Camera currently fixes the bird in the centre of the viewport. Intent was a **centre-third dead zone** — camera should not move until the bird reaches the edge of the centre third, reducing jitter. Logged as **ISS-79** (M-10).
- **3D follow (Human Gate)**: Follow does not work at all in 3D mode. Logged as **ISS-80** (M-10).
- **ISS-77** (Trail buffer overflow — segfault when drawing): deferred (Medium); address in a later milestone.
- **ISS-78** (Crash when switching to 3D after selecting bird with trail active): deferred (Medium); address in a later milestone.

### Process observations

### Ideas for rules or skills

---

## Promoted items

Items from the observations above that became actionable issues.

| Issue | Observation | Status |
|-------|-------------|--------|
| ISS-77 | Trail buffer overflow — segfault when drawing trajectory trail | Backlog (deferred) |
| ISS-78 | Crash when switching to 3D after selecting bird with trail active | Backlog (deferred) |
| ISS-79 | Follow (2D): use centre-third dead zone; camera moves only when bird leaves it | Backlog (M-10) |
| ISS-80 | Viewport follow does not work in 3D mode | Backlog (M-10) |
