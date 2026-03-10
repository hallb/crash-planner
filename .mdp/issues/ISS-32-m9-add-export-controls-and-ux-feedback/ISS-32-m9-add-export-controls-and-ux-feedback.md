---
id: ISS-32
title: "M9: Add export controls and UX feedback"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy: [ISS-29, ISS-30, ISS-31]
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T22:55:54.584Z
updatedAt: 2026-03-10T01:00:00.000Z
---

## Description

Add UI controls in the imgui controls panel for triggering exports and displaying status/error feedback. Depends on all export implementations being available (ISS-29, ISS-30, ISS-31).

**In scope:**
- "Export CSV/JSON" button: triggers data export; shows success path or error in UI
- "Start/Stop recording" toggle: arms the `RecordingBuffer` for video/GIF capture
- "Save MP4" and "Save GIF" buttons (available once recording is stopped)
- Output path display (from `ExportConfig.output_dir`)
- Status messages: success (with file path), in-progress spinner, error (e.g. ffmpeg missing)
- All export buttons disabled when a selection/recording state makes them invalid

**Acceptance:**
- Each export type triggerable from UI
- Errors (missing ffmpeg, write failure) surface as UI messages, not crashes
- Recording toggle correctly arms/disarms frame capture
