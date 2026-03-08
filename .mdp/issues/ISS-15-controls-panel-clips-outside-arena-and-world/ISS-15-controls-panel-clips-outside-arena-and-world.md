---
id: ISS-15
title: Controls panel clips outside arena and world sliders become unusable
type: bug
status: Done
priority: High
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
createdAt: 2026-03-08T15:14:15.943Z
updatedAt: 2026-03-08T19:17:46.915Z
---

## Origin
- **Found during**: M-2 Parameter tuning + perf stats
- **Related issue**: ISS-10 (ImGui parameter controls)

## Target Milestone
M-2 Parameter tuning + perf stats

## Description
Observed: The Controls panel renders over the simulation arena, can be dragged beyond the visible viewport where it becomes clipped, and in maximized/resized window states sliders can become unresponsive.

Expected: A fixed three-region layout where controls are docked in a dedicated non-overlapping sidebar, the simulation arena is clipped to its own region, and sliders remain usable at all window sizes.

## Steps to Reproduce
1. Launch the app.
2. Drag the Controls window toward/partially beyond the right edge of the viewport.
3. Attempt to adjust world width/height sliders.
4. Observe clipping and degraded/unusable interactions.

## Environment
- OS: Linux (WSL2)
- Renderer: Pygame + ModernGL + ImGui
- Typical runtime: 60 FPS / ~11 ms step

## Investigation
### Hypotheses
1. **Floating panel model is unstable under resize/maximize** — one-time placement with movable panel causes clipping and inconsistent input hit-testing
2. **No dedicated arena clipping** — agent rendering fills whole GL viewport so controls overlap arena

### Experiments
- Reviewed Controls implementation and verified `imgui.begin("Controls")` uses no fixed docking flags.
- Verified `_render_param_panel` sets position/size with `condition=imgui.ONCE`.
- Reviewed `Renderer2D.render` and confirmed full-screen draw without arena exclusion viewport/scissor.

## Resolution
### Root Cause
The overlay-based panel design allows controls to float over content and drift out of visible bounds. Combined with a full-screen render viewport, this creates overlap/clipping and unreliable interactions during maximize/resize transitions.

Additional confirmed root cause from runtime debugging:
- On this OPENGL + RESIZABLE path, `pygame.display.get_surface().get_size()` can remain stale after resize.
- ImGui `io.display_size` was therefore stuck at old dimensions, causing control hit-testing to diverge from the visible panel.

### Fix
- Adopt the solution-doc layout model: **arena (left)**, **controls sidebar (right)**, **metrics bar (bottom)**.
- Dock Controls to the right each frame (`ALWAYS`) and make it non-movable/non-resizable (`NO_MOVE | NO_RESIZE`).
- Enable resizable window handling and update renderer dimensions on `VIDEORESIZE` / `WINDOWSIZECHANGED`.
- Constrain agent drawing to the arena rect using GL viewport + scissor so rendering never overlaps controls/metrics.
- Source ImGui display sizing from `pygame.display.get_window_size()` and trust resize event dimensions (`event.w`/`event.h`) for `VIDEORESIZE`, avoiding stale surface-size reads.

## Verification
- Manual: Controls sidebar remains fixed on the right and fully visible.
- Manual: Bird arena is not covered by Controls or metrics bar.
- Manual: Sliders remain responsive in normal, resized, and maximized window states.
- Manual: World width/height controls remain usable.
- Automated: Existing test suite still passes.
- Runtime evidence: Debug instrumentation confirmed stale display-size readings before the fix and correct resize/dimension propagation after the fix.
- User confirmation: issue reproduced during investigation and later confirmed fixed after the final resize/display-size correction.

## Remaining Problems
World-boundary visualization behavior after resize is tracked separately in ISS-16. Parameter UX enhancements are tracked in ISS-17.