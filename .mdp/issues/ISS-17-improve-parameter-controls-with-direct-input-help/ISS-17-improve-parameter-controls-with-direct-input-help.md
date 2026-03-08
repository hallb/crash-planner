---
id: ISS-17
title: Improve parameter controls with direct input, help text, and reset
type: feature
status: Backlog
priority: Low
labels: []
assignee: null
milestone: null
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T15:15:29.041Z
updatedAt: 2026-03-08T23:29:48.962Z
---

## Description
Improve parameter controls usability by supporting direct numeric entry, inline explanatory help text, and per-parameter reset-to-default actions.

## Motivation
During M-2 human verification, slider-only controls were usable but limited for precise tuning and discoverability.

## Proposed scope
- Allow direct value entry in addition to sliders (e.g., input fields or ImGui slider text entry flow)
- Add concise explanatory text/tooltip for each parameter (what it does and practical effect)
- Add per-parameter reset controls to restore default values from `Configuration`

## Acceptance criteria
- Users can set exact parameter values without slider-only interaction
- Each parameter has accessible explanatory guidance
- Each parameter can be reset to its default without restarting