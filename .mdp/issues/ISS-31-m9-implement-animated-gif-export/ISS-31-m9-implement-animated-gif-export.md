---
id: ISS-31
title: "M9: Implement animated GIF export"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy: [ISS-81, ISS-82]
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T22:55:54.455Z
updatedAt: 2026-03-10T01:00:00.000Z
---

## Description

Consume frames from the `RecordingBuffer` (ISS-82) and assemble them into an animated GIF using Pillow (FR-023). Depends on ISS-81 (export config) and ISS-82 (frame capture).

**In scope:**
- Implement `encode_gif(frames, output_path, fps, frame_interval)` in `src/crash/data/export.py`
- Use `PIL.Image.save(..., save_all=True, append_images=..., loop=0)` 
- `frame_interval` (from `ExportConfig.gif_frame_interval`): only every Nth frame is included (default 2)
- 256-colour palette (Pillow default quantisation)
- Optionally cap output dimensions if config specifies a max size

**Acceptance:**
- GIF produced is a valid animated GIF (opens in standard viewers)
- Frame interval is respected (correct number of frames in output)
- Unit tests: write to temp file; assert file created, validate GIF header and frame count
