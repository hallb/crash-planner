---
id: ISS-82
title: "M9: Implement frame capture / recording buffer"
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
relatedTo: [ISS-30, ISS-31]
checklist: []
log: []
createdAt: "2026-03-10T01:00:00.000Z"
updatedAt: "2026-03-10T01:00:00.000Z"
---

## Description

Shared prerequisite for ISS-30 (MP4) and ISS-31 (GIF). Both formats require reading the rendered framebuffer each tick during a recording session. This issue implements that capture mechanism once, used by both export pipelines.

**In scope:**
- Implement a `FrameCapture` helper (or standalone function in `src/crash/data/`) that reads the OpenGL framebuffer pixel data after each render call and stores it as a raw bytes or numpy array
- Wire capture into the main loop: when recording is active, call capture after `renderer.render()` and before `renderer.flip()`
- Expose a `RecordingBuffer` — a bounded deque of captured frames — accessible to the export pipelines
- Add a recording-active flag to `ViewState` or a dedicated recording state object
- Unit test: mock framebuffer read; verify buffer fills, respects max-frame cap, and can be iterated by consumers
- No OpenGL context required in tests (mock `glReadPixels` / `ctx.screen`)

**Acceptance:**
- `RecordingBuffer` accumulates frames when active; discards oldest beyond cap
- Capture is wired into main loop behind a flag; no performance impact when inactive
- ISS-30 and ISS-31 depend on this issue; do not implement them until this is Done
