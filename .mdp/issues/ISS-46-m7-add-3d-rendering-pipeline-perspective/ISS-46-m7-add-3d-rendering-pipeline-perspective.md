---
id: ISS-46
title: "M7: Add 3D rendering pipeline (perspective projection, z-component in vertex data)"
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-50
parent: null
relatedTo: []
checklist: []
log:
  - "2026-03-09: Added 3D depth cues (atmospheric fog): v_depth varying + u_depth_fade uniform; birds far from camera fade toward background. Shader-only; 2D unchanged. See 04-front-end-design.md."
createdAt: 2026-03-09T01:36:10.081Z
updatedAt: 2026-03-09T01:40:36.937Z
---

## Description

Replace orthographic projection with perspective projection when dimensions=3. Upload z-component of agent positions to GPU vertex buffer. Update vertex shader to accept and use z-coordinate. Keep orthographic path for 2D mode. No new agent geometry needed — instanced draw continues.

Per FR-001 (system renders agents in 3D space per FR-027). Frame rate must remain ≥30 FPS at default agent count per NFR-001. Renderer must not contain simulation logic per NFR-013.

### Notes from ISS-50 spike

- Add `pygame.display.gl_set_attribute(pygame.GL_DEPTH_SIZE, 24)` before `set_mode()` (or before context create). Clear `GL_DEPTH_BUFFER_BIT`; enable depth test for scene, disable for ImGui.
- Shader: change instance layout to `3f` (x,y,z); replace orthographic MVP with perspective when dimensions=3; fragment shader unchanged.
- ImGui overlay composes correctly (depth disabled for ImGui draw).
- Agent geometry: flat triangles in 3D space; add z to instance pos; no billboarding needed for M-7.
