---
id: ISS-37
title: "M6: Widen FlockingAlgorithm protocol params type and add Flock2Params dataclass"
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
createdAt: 2026-03-09T01:35:39.346Z
updatedAt: 2026-03-09T15:43:21.658Z
---

## Description

Introduce a base AlgorithmParams type (or union) so the FlockingAlgorithm protocol step() is not hardcoded to BoidsParams. Add Flock2Params dataclass to the data layer with fields: neighbour_count (int), thrust (float), drag (float), field_of_view (float). Widen SimulationState or params plumbing accordingly.
