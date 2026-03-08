---
id: ISS-8
title: Add pyimgui and ImGui overlay integration
type: task
status: Done
priority: null
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
createdAt: 2026-03-08T02:03:19.237Z
updatedAt: 2026-03-08T03:30:00.000Z
---

## Description

Add pyimgui to deps; integrate with Pygame+ModernGL render loop; render imgui frame each tick. Per 02-tech-stack, 04-front-end-design.

**Note (NFR-015):** Verify that pyimgui has no new system-level dependencies beyond what `script/bootstrap` already installs (`libgl-dev`, `libegl-dev`). If additional packages are required, update `script/bootstrap` accordingly.

## Implementation notes

### Package name

The package on PyPI is `imgui` (version 2.0.0), not `pyimgui`. The `pyimgui` name was retired; `imgui` is the continuation. Added as `imgui[full]` in `pyproject.toml`.

### Additional system dependency: `python3-dev`

`imgui` is a Cython C extension and requires Python development headers (`Python.h`) to compile from source. Added `python3-dev` (apt) / `python3-devel` (dnf) to `script/bootstrap`.

### GL_ALPHA incompatibility with OpenGL Core Profile 3.3

**Problem:** The `imgui` package's `PygameRenderer` inherits from `FixedPipelineRenderer`, which uses `GL_ALPHA` as the font texture internal format (`glTexImage2D(..., GL_ALPHA, ...)`). `GL_ALPHA` was deprecated in OpenGL 3.0 and **removed from Core Profile 3.3+**, causing a `GLError(err=1281, GL_INVALID_VALUE)` on startup.

Our renderer uses Core Profile 3.3 (correct for future 3D support — see ADR-002), so this is not negotiable.

**Fix:** Introduced `_CorePygameRenderer(ProgrammablePipelineRenderer)` in `renderer_2d.py`. `ProgrammablePipelineRenderer` already uses `GL_RGBA` (valid in Core Profile) for the font texture. The class copies the pygame event/input handling from `PygameRenderer` (key map, mouse events, delta time). No library files modified; no downgrade to Compatibility Profile.

**Summary of class hierarchy:**

```
# imgui package (what we can't use directly):
PygameRenderer → FixedPipelineRenderer   ← uses GL_ALPHA (invalid in Core Profile)

# Our fix:
_CorePygameRenderer → ProgrammablePipelineRenderer  ← uses GL_RGBA (Core Profile safe)
                      + pygame event handling copied from PygameRenderer
```

This approach is forward-compatible with future OpenGL upgrades (3D mode, M-7).

### PyOpenGL context detection failure on WSL2/EGL (second fix)

**Problem:** At runtime (`./script/server`), the `_CorePygameRenderer.__init__()` call still crashed:

```
OpenGL.error.Error: Attempt to retrieve context when no valid context
  glVertexAttribPointer → contextdata.getContext → platform.GetCurrentContext() → NULL
```

`ProgrammablePipelineRenderer._create_device_objects()` calls PyOpenGL's `gl.*` functions, which use `glXGetCurrentContext()` (the GLX platform) to locate the active OpenGL context. On WSL2, SDL2/pygame creates the window via an **EGL context** (not GLX). `glXGetCurrentContext()` returns NULL for an EGL context, so PyOpenGL cannot find the context even though it is fully initialised.

**Root cause:** PyOpenGL (on Linux) defaults to the GLX platform. The EGL context created by SDL2/Wayland is invisible to `glXGetCurrentContext()`, regardless of whether imgui is initialised before or after `moderngl.create_context()`.

**Fix:** Replaced `_CorePygameRenderer` (which inherits `ProgrammablePipelineRenderer` from PyOpenGL) with a fully self-contained `_ImguiRenderer` class that uses **ModernGL only** — no PyOpenGL imports anywhere in the imgui rendering path. ModernGL already holds the EGL context correctly (proven by M-1), so this resolves the conflict at the root.

**Summary of final class design:**

```
# Old approach (broken on WSL2/EGL):
_CorePygameRenderer → ProgrammablePipelineRenderer → PyOpenGL gl.* → glXGetCurrentContext() → NULL

# New approach:
_ImguiRenderer
  ├── process_event / process_inputs  ← pygame event handling (same logic as before)
  └── render(draw_data)               ← ModernGL: shader, VBO/IBO/VAO, font texture
                                         vertex data converted numpy uint8→float32
                                         no PyOpenGL dependency anywhere
```

Key implementation details:
- Font atlas uploaded as RGBA32 via `ctx.texture()` (Core Profile safe, same as before).
- ImGui's packed `uint8` colour channel converted to `float32` on CPU via numpy before upload, avoiding ModernGL normalised-integer attribute complexity.
- Scissor per draw command via `ctx.screen.scissor = (x, y, w, h)` / `= None`.
- Projection matrix: orthographic top-left → NDC, uploaded as `mat4` uniform.
