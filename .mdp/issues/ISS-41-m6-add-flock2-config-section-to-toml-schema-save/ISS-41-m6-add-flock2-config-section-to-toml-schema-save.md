---
id: ISS-41
title: "M6: Add Flock2 config section to TOML schema (save/load)"
type: task
status: Done
priority: null
labels: []
assignee: null
milestone: M-6
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-09T01:35:52.617Z
updatedAt: 2026-03-09T15:47:35.801Z
---

## Description

Extend TOML config schema with a [flock2] section: neighbour_count (int), thrust (float), drag (float), field_of_view (float). Wire save/load so Flock2 params round-trip correctly. Extend config validation and defaults. Per NFR-011 (config round-trip fidelity).
