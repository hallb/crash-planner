---
id: ISS-16
title: Window resize support and world boundary behavior
type: feature
status: Backlog
priority: Medium
labels: []
assignee: null
milestone: ""
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T15:15:19.232Z
updatedAt: 2026-03-09T20:08:05.161Z
---

## Description
Support resizable app windows and define clear behavior when window size differs from simulation world dimensions.

## Motivation
During M-2 human verification, resizing the main window exposed ambiguity around world bounds visibility and how world size should react to window changes.

## Proposed scope
- Add resizable window support (`pygame.RESIZABLE`)
- Handle `VIDEORESIZE` events and propagate new viewport dimensions to renderer and controls layout
- Choose and implement one behavior for world mismatch:
  1. Auto-fit world dimensions to viewport (minus Controls sidebar + metrics bar), or
  2. Keep world fixed and draw a clear world boundary indicator when viewport exceeds world

## Acceptance criteria
- Resizing the window does not break rendering or controls layout
- Controls and metrics remain fully visible and correctly placed
- Chosen world mismatch behavior is consistent and documented

## Progress update (post ISS-15 fix)
- Implemented: resizable window plumbing and resize propagation to renderer/controls layout.
- Implemented: controls and metrics placement now remain stable during resize/maximize.
- Remaining (keeps this issue in Backlog): choose and implement final world mismatch behavior (auto-fit world vs explicit world boundary indicator), then document that behavior.