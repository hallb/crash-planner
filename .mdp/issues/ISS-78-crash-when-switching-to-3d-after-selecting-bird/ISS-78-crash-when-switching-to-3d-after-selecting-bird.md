---
id: ISS-78
title: Crash when switching to 3D after selecting bird with trail active
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
  - timestamp: 2026-03-09T21:26:40.913Z
    author: cli
    body: "Initial hypothesis: trail_deque mixes 2D and 3D points across dimension switch (inhomogeneous sequence)."
  - timestamp: 2026-03-09T21:26:50.321Z
    author: cli
    body: "Bug reported: 2D trail active -> switch to 3D crashes with ValueError at np.array(trail_deque, dtype=np.float64)."
  - timestamp: 2026-03-10T18:49:00.000Z
    author: cli
    body: "Verified resolved: main.py _update_follow_and_trail clears trail_deque and trail_buffer when len(trail_deque[-1]) != len(pos), so 2D->3D (or 3D->2D) never leaves inhomogeneous points for np.array. Marked Done."
createdAt: 2026-03-09T21:26:15.087Z
updatedAt: 2026-03-10T18:49:29.262Z
---

## Origin

- **Found during**: M-5 manual verification (follow/trail behavior)
- **Related issue**: ISS-59 (trail render), ISS-76 (2D/3D telemetry behavior), ISS-77 (trail stability)

## Target Milestone

M-5

## Description

**Observed**: After selecting a bird (trail visible) and switching to 3D, the app crashes in `_update_follow_and_trail`.

**Expected**: Switching from 2D to 3D should not crash; trail and selection state should be reset or normalized safely.

Crash trace from user:

```text
Traceback (most recent call last):
  File "/home/hallb/work/aisdlc/crash/main.py", line 9, in <module>
    main()
  File "/home/hallb/work/aisdlc/crash/src/crash/main.py", line 94, in main
    _update_follow_and_trail(engine.state, view_state, trail_deque)
  File "/home/hallb/work/aisdlc/crash/src/crash/main.py", line 137, in _update_follow_and_trail
    arr = np.array(trail_deque, dtype=np.float64)
ValueError: setting an array element with a sequence. The requested array has an inhomogeneous shape after 1 dimensions. The detected shape was (200,) + inhomogeneous part.
```

## Steps to Reproduce

1. Run the app: `./script/server`
2. In 2D mode, select an agent so trail rendering starts
3. Switch dimensions from 2D to 3D
4. Observe crash with `ValueError` at `arr = np.array(trail_deque, dtype=np.float64)`

## Environment

- Linux (WSL2), pygame 2.6.1, Python 3.12.3
- Branch: `feature/M-5-follow-trail`

## Investigation

### Hypotheses

1. **H1 (mixed point dimensionality in trail deque)** — Trail deque contains 2D points from 2D mode, then receives 3D points after switching to 3D, producing an inhomogeneous sequence that NumPy cannot convert to a single float array. **LIKELY** (consistent with traceback and error text).
2. **H2 (stale trail not cleared on dimension switch)** — Switching dimensions does not clear `trail_deque` / `view_state.trail_buffer` before appending points in the new dimensionality. **LIKELY**.
3. **H3 (unexpected non-numeric payload in trail deque)** — Non-list/non-numeric value inserted into trail deque. **INCONCLUSIVE** (no evidence yet).

### Experiments

- Runtime traceback captured from user session (above).
- Code path implicated: `main.py:_update_follow_and_trail` on `np.array(trail_deque, dtype=np.float64)`.

## Resolution

### Root Cause

Pending implementation.

### Fix

Pending implementation.

## Verification

Pending implementation.

## Remaining Problems

Open. Crashes reliably on 2D -> 3D switch when a trail already exists.
