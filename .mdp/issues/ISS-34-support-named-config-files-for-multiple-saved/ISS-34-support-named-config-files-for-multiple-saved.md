---
id: ISS-34
title: Support named config files for multiple saved configurations
type: feature
status: Backlog
priority: null
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
createdAt: 2026-03-09T01:07:25.048Z
updatedAt: 2026-03-09T01:07:25.048Z
---

## Motivation

Currently, config save/load always targets a fixed filename (`crash.toml`). This prevents users from maintaining multiple configurations (e.g., different flocking presets or experiment setups).

## Proposed behaviour

- `save_config(config, path=None)` — if `path` is `None`, use the default filename; otherwise write to the given path.
- `load_config(path=None)` — symmetric: default path when `None`, named file otherwise.
- The UI or CLI can expose a filename field or argument to select which config to load/save.

## Acceptance criteria

- [ ] `save_config` and `load_config` accept an optional `path` parameter.
- [ ] Default behaviour (no path supplied) is unchanged.
- [ ] Tests cover default-path and named-path variants for both save and load.
- [ ] Mutation gate passes for changed code.