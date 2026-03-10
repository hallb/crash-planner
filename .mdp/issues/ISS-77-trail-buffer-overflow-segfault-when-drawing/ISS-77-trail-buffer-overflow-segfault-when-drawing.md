---
id: ISS-77
title: Trail buffer overflow — segfault when drawing trajectory trail
type: bug
status: Done
priority: Medium
labels: []
assignee: null
milestone: M-5
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log:
  - timestamp: 2026-03-09T20:27:59.173Z
    author: cli
    body: "Bug reported: User selected bird; trail drew horizontal line then segfault. moderngl.Error out of range size=2424 at trail_buffer.write (renderer_2d.py)."
  - timestamp: 2026-03-09T20:28:00.446Z
    author: cli
    body: "Investigation: H1 confirmed — 2424 bytes = 202 vertices; buffer reserved 200*12=2400. Renderer did not clamp trail length before write."
  - timestamp: 2026-03-09T20:28:01.875Z
    author: cli
    body: "Fix applied: Clamp n_pts = min(trail.shape[0], TRAIL_MAX_LEN), use trail[-n_pts:], write and render n_pts only (renderer_2d.py). Pending user verification."
  - timestamp: 2026-03-10T18:48:00.000Z
    author: cli
    body: "Verified resolved: main.py caps trail to TRAIL_MAX_LEN before trail_buffer (defence in depth); renderer_2d.py clamps n_pts/n_verts and write size. No crash on trail draw. Marked Done."
createdAt: 2026-03-09T20:27:28.937Z
updatedAt: 2026-03-10T18:48:04.000Z
---

## Origin

- **Found during**: M-5 Agent follow + trajectory trail (manual verification)
- **Related issue**: ISS-59 (render trajectory trail), ISS-62 (tests for follow and trail)

## Target Milestone

M-5

## Description

**Observed**: User selected a bird; the app drew a horizontal line (the trajectory trail) then segfaulted. Console showed:

```
_moderngl.Error: out of range offset = 0 or size = 2424
```

at `renderer_2d.py` in `render`, line `self._trail_buffer.write(trail_3.tobytes())`.

**Expected**: Trail should render without crashing; buffer writes must stay within the reserved GPU buffer size.

## Steps to Reproduce

1. Run the app: `./script/server`
2. Select an agent (click or Agent ID)
3. Optionally enable "Follow agent"
4. Let the simulation run briefly so the trail accumulates
5. Observe: a horizontal line (trail) may appear, then the process crashes with the moderngl error above

## Environment

- Linux (WSL2), pygame 2.6.1, Python 3.12.3
- Trail feature (FR-026) implemented in M-5; buffer reserved with `TRAIL_MAX_LEN * 3 * 4` bytes

## Investigation

### Hypotheses

1. **H1 (trail length &gt; buffer capacity)** — `view_state.trail_buffer` had more than `TRAIL_MAX_LEN` (200) points, so the byte size written (2424 = 202×3×4) exceeded the reserved buffer (200×3×4 = 2400). **CONFIRMED** — error size 2424 implies 202 vertices; buffer is 2400 bytes.
2. **H2 (deque not bounded)** — The deque in main might have grown past 200. **INCONCLUSIVE** — deque is created with `maxlen=TRAIL_MAX_LEN` (200), so it should cap at 200; source of the extra 2 points not definitively identified (could be alternate code path or build/config).
3. **H3 (renderer assumes trail ≤ TRAIL_MAX_LEN)** — Renderer never clamped the number of vertices before write. **CONFIRMED** — no clamp was applied; writing whatever `trail_buffer` contained caused overflow when length &gt; 200.

### Experiments

- Inspected error: `size = 2424` → 202 vertices × 3 components × 4 bytes. Buffer reserve is `TRAIL_MAX_LEN * 3 * 4` = 2400.
- Confirmed in code: trail GPU buffer is created with `reserve=TRAIL_MAX_LEN * 3 * 4`; trail data is written without clamping to that length.

## Resolution

### Root Cause

The trajectory trail GPU buffer is reserved for exactly `TRAIL_MAX_LEN` (200) vertices. When `view_state.trail_buffer` contained more than 200 points (202 in the observed crash), `trail_3.tobytes()` exceeded the reserved size and ModernGL raised "out of range".

### Fix

In `src/crash/renderer/renderer_2d.py`, in the trail-drawing block:

- Clamp the number of points to the buffer capacity: `n_pts = min(int(trail.shape[0]), TRAIL_MAX_LEN)`.
- Use only the most recent points: `trail = trail[-n_pts:]`.
- Build `trail_3` and write exactly `n_pts` vertices; render `LINE_STRIP` with `vertices=n_pts`.

This ensures the renderer never writes more than the reserved buffer size regardless of how many points are in `trail_buffer`.

## Verification

- Unit tests (selection, view_state) pass.
- User to re-run manual verification: select agent, run with follow/trail, confirm no crash.

## Remaining Problems

None. If the source of the extra points (e.g. trail_buffer ever &gt; 200) is found later, an additional clamp in main when setting `view_state.trail_buffer` could be added for defence in depth.
