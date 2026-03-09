---
id: ISS-51
title: Enhance 3D visual depth cues (richer bird geometry, bounding box, size attenuation)
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-10
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo:
  - ISS-46
checklist: []
log: []
createdAt: 2026-03-09T00:00:00.000Z
updatedAt: 2026-03-09T03:36:03.707Z
---

## Description

M-7 added a perspective projection and atmospheric depth fade (near = bright, far = dim) to make the 3D mode visually distinguishable from 2D. Additional depth cues would make the 3D volume more legible and the simulation more visually engaging.

### Candidate improvements (pick any subset)

**Richer bird geometry**
- Replace the flat 2-triangle arrow with a 3D wedge or cone (3–6 triangles). Normals would enable basic diffuse shading: a fixed "sun" direction gives a light face and a dark face, providing immediate shape and depth cues with no extra CPU cost.
- Alternative: billboarded sprites (texture quad always facing camera).

**Wireframe bounding box**
- Draw the world-volume edges as 12 line segments in a distinct colour (e.g., dim grey). Gives the viewer a fixed spatial reference for where the birds are in depth. Rendered as a second VAO with `GL_LINES`; does not require normals or depth shading changes.

**Size attenuation beyond perspective**
- The perspective matrix already shrinks distant birds, but with the current wide camera distance the effect is subtle. Reducing camera distance or increasing FOV would amplify it. Alternatively, scale the instance `scale` uniform with a Z-based factor in the vertex shader.

**Orbit camera controls** (already planned as ISS-47 / Phase 10)
- Mouse-drag yaw/pitch around the flock centroid is the single most impactful depth cue — parallax immediately communicates 3D structure. Tracked in ISS-47.

### Acceptance criteria

- At least one of the above improvements is implemented and visually demonstrable.
- 2D mode is unchanged.
- Frame rate remains ≥30 FPS at default agent count (NFR-001).
- `./script/cibuild` exits 0.
