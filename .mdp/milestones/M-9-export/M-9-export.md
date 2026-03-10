---
id: M-9
title: Export
status: Planning
priority: null
labels: []
startDate: null
dueDate: null
checklist: []
log: []
createdAt: "2026-03-07T00:00:00.000Z"
updatedAt: "2026-03-10T01:00:00.000Z"
---

#### Milestone Identity

**Milestone ID**: M-9
**Milestone Name**: Export
**FR Mapping**:
- FR-021 (partial: `[export]` config section — output path, formats, GIF frame interval)
- FR-022 Animation export: Video (MP4 via ffmpeg)
- FR-023 Animation export: GIF (Pillow)
- FR-024 Data export (CSV and JSON, 2D and 3D)
- NFR-008 Export completion time

#### Goal

The user can export per-frame agent positions and velocities to CSV or JSON, and export a recorded simulation clip as MP4 video or animated GIF, from either 2D or 3D mode with either algorithm.

#### Dependencies

M-3 (Config persistence + pause)

#### Plan

1. Add `[export]` config section and `ExportConfig` data model; extend `config_io.py` save/load (ISS-81)
2. Implement frame capture / recording buffer consumed by video and GIF pipelines (ISS-82)
3. Implement CSV and JSON data export in `src/crash/data/export.py`, covering 2D and 3D state (ISS-29)
4. Implement MP4 export via ffmpeg subprocess with graceful degradation when ffmpeg is absent (ISS-30)
5. Implement animated GIF export via Pillow with configurable frame interval (ISS-31)
6. Add export UI controls: data export buttons, recording start/stop toggle, MP4/GIF save buttons, status feedback (ISS-32)
7. Add format-correctness tests, NFR-008 performance benchmarks, 2D/3D coverage, and mutation gate (ISS-33)

#### Outcome

- `[export]` TOML section supported in config schema; saves and loads correctly
- Frame capture buffer wired into main loop; inactive when recording is off
- CSV export produced with correct 2D/3D column schema
- JSON export produced with correct 2D/3D object schema
- MP4 export produced when ffmpeg available; graceful warning when absent
- Animated GIF export produced with configurable frame interval
- All exports accessible from UI; errors surface as messages, not crashes
- NFR-008 performance targets met or limits documented

#### Automated Verification (AI Gate)

1. Run full test suite: `./script/cibuild` — all tests pass
2. CSV/JSON tests: assert column headers for 2D and 3D fixtures
3. GIF test: assert valid GIF header and correct frame count
4. MP4 test: assert ffmpeg subprocess invoked with correct args (mocked)
5. Performance benchmarks: data export ≤ 30 s for 36,000 frames (100 agents × 10 min at 60 fps); video throughput ≥ 0.5× real-time (or limits documented)
6. Mutation gate: `./script/mutate --scope src/crash/data/export.py` — survivors killed or documented

**Expected**:
- All 6 steps pass
- Coverage ≥ 60% on `src/crash/data/export.py`

#### Human Verification (Human Gate)

1. Trigger CSV/JSON export from UI; open output files and verify columns and data for both 2D and 3D modes
2. Start and stop recording; save as MP4; verify video plays in a standard media player
3. Start and stop recording; save as GIF; verify GIF animates in a standard viewer
4. Verify export works for both Boids and Flock2 algorithms

#### Success Criteria

✅ `[export]` config section saves and loads correctly
✅ CSV export of per-frame positions/velocities with correct 2D and 3D schema
✅ JSON export of per-frame positions/velocities with correct 2D and 3D schema
✅ MP4 export works when ffmpeg available; app does not crash when ffmpeg absent
✅ Animated GIF export works with configurable frame interval
✅ All exports triggerable from UI with clear feedback
✅ NFR-008 performance targets met or limits documented
✅ All tests pass; export code mutation-gated
