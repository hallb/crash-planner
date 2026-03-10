---
id: ISS-30
title: "M9: Implement MP4 export pipeline via ffmpeg"
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-81
  - ISS-82
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T22:55:54.347Z
updatedAt: 2026-03-10T01:44:06.639Z
---

## Description

Consume frames from the `RecordingBuffer` (ISS-82) and pipe them to ffmpeg via subprocess to produce a playable MP4 file (FR-022). Depends on ISS-81 (export config) and ISS-82 (frame capture).

**In scope:**
- Implement `encode_mp4(frames, output_path, fps, resolution)` in `src/crash/data/export.py`
- Pipe raw RGB bytes to `ffmpeg -f rawvideo -pix_fmt rgb24 ... -vcodec libx264 output.mp4` via `subprocess.run`
- Resolution matches window size or `ExportConfig.video_resolution`
- **Graceful degradation:** if ffmpeg is not found on PATH, log a clear error and surface it to the UI as a warning — do not crash; export attempt is silently skipped with a user-visible message
- Document ffmpeg as an optional system dependency in `docs/02-solution/08-infrastructure.md` (or equivalent)

**Performance target (NFR-008):** Video export completes within 2× real-time of the exported duration. Document limits if the target cannot be met in WSL2.

**Acceptance:**
- MP4 produced and playable when ffmpeg is available
- App does not crash when ffmpeg is absent; warning is shown
- Unit tests: mock `subprocess.run`; assert correct ffmpeg args and graceful-degradation path
