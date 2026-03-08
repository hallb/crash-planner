---
id: ISS-7
title: Birds disappear at viewport edge (visualization)
type: bug
status: Backlog
priority: Medium
labels: []
assignee: null
milestone: M-2
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T01:24:16.581Z
updatedAt: 2026-03-08T01:24:16.581Z
---

## Origin

- **Found during**: M-1 MVP Boids 2D
- **Related issue**: (general visual verification during M-1 completion)

## Target Milestone

M-2 Parameter tuning & perf stats

## Description

**Observed**: Agents reaching the world edge turn around (boundary steering works) but disappear from view before reappearing.

**Expected**: Birds should remain visible at all times; they may turn at the edge but should not vanish.

Rendering/viewport clipping or projection issue in the 2D renderer.

## Steps to Reproduce

1. Run the app: `./script/server` or `uv run python main.py`
2. Let the simulation run until birds reach the viewport edges (they turn around near the boundary)
3. Observe: birds disappear before reappearing (most noticeable at bottom and right edges)

## Environment

- World size: 800×600
- Agent count: 10 (or 100)
- OS: Linux (WSL2)

## Investigation

### Hypotheses

1. **H1 (NDC clipping)** — Orthographic projection maps world [0,w]×[0,h] to NDC [-1,1]. Agents or triangle vertices outside that range get clipped by the GPU. **CONFIRMED** via logs: `sample_ndc_y` < -1 when agent y > 600; `sample_ndc_x` > 1 when agent x > 808.
2. **H2 (Projection matrix layout)** — MVP row/column-major mismatch. **REJECTED** — NDC math matches.
3. **H3 (Viewport mismatch)** — ModernGL viewport not covering full window. **REJECTED** — clipping is in NDC.
4. **H4 (Y-axis boundary)** — Same as H1 for y. **CONFIRMED**.
5. **H5 (Agent scale at edges)** — Triangle extent (~4 world units) plus positions past bounds cause clipping. **CONFIRMED**.

### Experiments

- Instrumented `renderer_2d.py` with NDJSON logs: agent positions, edge counts, sample NDC coords, `would_clip_x`.
- Logs showed agents at y=600–602 mapping to NDC y < -1; agents at x=804–860 mapping to NDC x > 1.
- Boundary steering allows overshoot (margin=50); agents can exceed world bounds before turning.

## Resolution

### Root Cause

Orthographic projection mapped world [0,w]×[0,h] to NDC [-1,1]. Agents and their triangle vertices that extended past the world bounds (due to boundary overshoot and triangle extent) mapped outside NDC and were clipped by the GPU.

### Fix

Extended orthographic projection view volume by margin 70 (covers boundary zone + triangle extent). Changed `left, right = 0, w` to `left, right = -margin, w + margin`; same for y. File: `src/crash/renderer/renderer_2d.py`.

## Verification

Post-fix runs showed improvement: bottom-edge clipping largely resolved; right-edge clipping resolved. Logs confirmed agents at previously problematic positions now map within NDC.

## Remaining Problems

- Occasional disappearance still observed on bottom edge in latest run, not consistently reproducible.
- May need larger margin, or alternative approach (e.g. clamp positions for rendering only, or soft boundary).
