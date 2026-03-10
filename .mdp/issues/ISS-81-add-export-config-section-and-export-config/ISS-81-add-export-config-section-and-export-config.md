---
id: ISS-81
title: "M9: Add [export] config section and export config data model"
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-9
estimate: null
spent: null
dueDate: null
blockedBy: []
parent: null
relatedTo: [ISS-29, ISS-30, ISS-31]
checklist: []
log: []
createdAt: "2026-03-10T01:00:00.000Z"
updatedAt: "2026-03-10T01:00:00.000Z"
---

## Description

Prerequisite for all M-9 export tasks. The solution design specifies an `[export]` TOML section (output path, format options, GIF frame sampling rate). This issue adds that section to the config schema and wires it into the data layer before any export implementation begins.

**In scope:**
- Add `[export]` TOML section to `crash/docs/02-solution/06-data-design.md` parameter table (document the full schema)
- Extend `Config` dataclass in `src/crash/data/config.py` with an `ExportConfig` sub-object (or flat fields): `output_dir: Path`, `data_formats: list[str]` (csv, json), `video_enabled: bool`, `gif_enabled: bool`, `gif_frame_interval: int`
- Add validation for unknown keys and range checks (e.g. `gif_frame_interval >= 1`)
- Add round-trip save/load support in `config_io.py` for the `[export]` section
- Add unit tests: save, load, round-trip, validation errors

**Acceptance:**
- `Config` carries an `ExportConfig` with defaults
- Save/load round-trip preserves all export fields
- Unknown `[export]` keys raise `ConfigError`
- Tests pass; coverage ≥ 80% on new code
