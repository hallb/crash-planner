---
id: ISS-39
title: "M6: Add algorithm registry and wire engine to use it"
type: task
status: Backlog
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
createdAt: 2026-03-09T01:35:39.458Z
updatedAt: 2026-03-09T01:35:39.458Z
---

## Description

Add REGISTRY = {"boids": BoidsAlgorithm, "flock2": Flock2Algorithm} populated at import time. Engine selects algorithm by key. Switching algorithm resets and restarts simulation with current parameter set (new positions, re-seeded). Per NFR-006: new algorithms added without modifying existing algorithm code.
