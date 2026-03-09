---
id: ISS-50
title: "M7: Spike — trial 3D rendering with Pygame/ModernGL/pyimgui"
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-7
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:40:33.273Z
updatedAt: 2026-03-09T01:40:33.273Z
---

## Questions to answer

1. Does the existing Pygame/ModernGL window setup support depth buffering, or does OpenGL context creation need rework?
2. Can the current shader pipeline adapt to perspective projection and 3D vertex data, or does it need a rewrite?
3. Does the pyimgui overlay still compose correctly over a 3D viewport with depth testing enabled?
4. What does instanced 3D agent rendering look like — flat triangles in 3D space, or do we need real geometry?

## Deliverables

- Documented answers to the four questions above
- Findings recorded as notes on ISS-46 (rendering pipeline) and ISS-48 (toggle UI)
- Any code written during the spike is discarded — it is not committed or carried forward

## Definition of done

Findings documented; dependent issues unblocked.

---

## Spike findings (completed)

### 1. Does the existing Pygame/ModernGL window setup support depth buffering?

**No.** The current setup uses `pygame.display.set_mode(..., pygame.OPENGL | pygame.DOUBLEBUF | pygame.RESIZABLE)` without requesting a depth buffer. No `pygame.display.gl_set_attribute(pygame.GL_DEPTH_SIZE, ...)` is set before `set_mode()`. SDL2 may provide a default depth buffer on some platforms, but it is not guaranteed.

**Action for ISS-46:** Add `pygame.display.gl_set_attribute(pygame.GL_DEPTH_SIZE, 24)` before `set_mode()` when 3D mode is supported. In the render path: clear with `GL_DEPTH_BUFFER_BIT`, enable `GL_DEPTH_TEST` for the scene draw, disable for ImGui (ImGui already disables depth test).

### 2. Can the current shader pipeline adapt to perspective projection and 3D vertex data?

**Yes, with targeted changes.** The agent vertex shader currently uses `in vec2 in_instance_pos` and orthographic MVP. To adapt: (a) change instance layout to `3f` (x, y, z); (b) replace orthographic MVP with a perspective view×projection matrix when dimensions=3; (c) pass z through to `gl_Position`. The fragment shader can remain unchanged. No full rewrite—localised edits to vertex shader, instance buffer format, and MVP construction.

### 3. Does the pyimgui overlay still compose correctly over a 3D viewport with depth testing enabled?

**Yes.** The ImGui renderer explicitly disables `moderngl.DEPTH_TEST` and draws after the scene. Standard pattern: draw 3D scene with depth test enabled, then draw ImGui with depth test disabled on top. No changes needed.

### 4. What does instanced 3D agent rendering look like — flat triangles in 3D space, or do we need real geometry?

**Flat triangles in 3D space.** The current geometry is triangles in the XY plane, rotated by angle and positioned. For 3D: add z to instance position (`in_instance_pos` becomes vec3), keep the same local triangle. World position becomes `vec4(rotated * scale + in_instance_pos.xy, in_instance_pos.z, 1.0)`. Triangles will appear edge-on (thin lines) when viewed from the side—acceptable per ISS-46 ("No new agent geometry needed"). Billboarding can be deferred to a later improvement.