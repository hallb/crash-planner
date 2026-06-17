---
id: ISS-89
title: "UX review: improve control panel readability and discoverability"
type: task
status: Backlog
priority: Medium
labels:
  - enhancement
  - frontend
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
createdAt: 2026-03-11T19:25:38.782Z
updatedAt: 2026-03-11T19:25:38.782Z
---

## Context

UX review of the current control panel UI against requirements in `docs/01-requirements/`.
The panel is functional but has several readability and discoverability issues
that reduce the quality of the experience for both the developer/learner (primary
stakeholder) and the demo viewer (STK-001).

Screenshot reviewed: the right-side control panel showing Controls, Export, Global,
and Boids sections with buttons, dropdowns, and sliders.

---

## Issues identified

### 1. Truncated parameter labels (high impact)

Nearly every slider label is clipped: "World dep", "Agent cou", "World wic",
"Max spec", "Min spec", "Separatic", "Protectec", "Turn fact", "Visual ra".
The user cannot read what parameter they are adjusting without guessing.

**Affected requirements:** FR-002, FR-003, NFR-007 (visible feedback within 100 ms
of user action — truncated labels defeat feedback because the user cannot identify
the control).

**Suggestions:**
- Widen the panel or use a two-row layout (label above, slider below) so labels
  are never clipped.
- Use concise but unambiguous short names (e.g., "Sep. Weight", "Align Weight",
  "Cohesion", "Max Speed", "World W", "World H", "World D", "Agents").
- Consider tooltips on hover showing the full parameter name and valid range.

### 2. No units or valid-range hints on sliders

Slider values display raw numbers (e.g., 600.000, 0.050) with no unit or range
context. A user cannot tell whether "World dep: 600.000" means pixels, metres,
or arbitrary units, nor what the min/max bounds are.

**Affected requirements:** FR-002 acceptance criterion (invalid values produce error
per NFR-005) — the user lacks context to choose valid values.

**Suggestions:**
- Show units after the value where applicable (e.g., "600 units", "3.0 u/s").
- Display min/max bounds on the slider track or in a tooltip.

### 3. Inconsistent numeric precision

"Agent cou" (agent count) shows as an integer while other parameters show three
decimal places (e.g., 0.050). Agent count should never display decimal places.
Weights that are small floats may benefit from fewer decimals (e.g., 0.05 not 0.050).

**Suggestions:**
- Use integer formatting for discrete parameters (agent count, world dimensions).
- Use 2–3 significant digits for weights/factors; drop trailing zeroes.

### 4. "Agent ID" and "Select by ID" buttons are ambiguous

Two separate buttons exist but their distinct purpose is unclear from labels alone.
FR-010 says the user can select an agent by entering a numeric ID — presumably one
of these opens an input field — but which one?

**Suggestions:**
- Rename to clarify intent: e.g., "Show Agent ID" (displays the selected agent's ID)
  vs "Go to Agent #" (opens a numeric input to select by ID).
- Consider merging into a single input field with a label like "Agent #" that both
  displays the current selection and accepts typed input.

### 5. Export section UX

- The output path displays a truncated absolute filesystem path
  (`/home/hallb/work/aisdl`). This is unfriendly and leaks system details.
- "(record first)" hint below "Start recording" is cryptic — it is unclear whether
  this is an instruction, a status, or a prerequisite.

**Affected requirements:** FR-022, FR-023, FR-024.

**Suggestions:**
- Show a relative or shortened path, or provide a file-chooser interaction.
- Replace "(record first)" with a clearer status/instruction, e.g.,
  "Record a session before exporting video/GIF" or grey out export buttons until
  a recording exists.

### 6. Algorithm dropdown label truncation

The algorithm selector area shows "Boids" in one dropdown and "Algorithm" as a
label that appears clipped on the adjacent dropdown. The relationship between the
two dropdowns (one for algorithm, one for dimensionality?) is unclear.

**Affected requirements:** FR-007 ("selected algorithm is clearly indicated"),
FR-027 ("selected mode is clearly indicated").

**Suggestions:**
- Label each dropdown explicitly: "Algorithm: [Boids]" and "Dimension: [3D]".
- Ensure labels are not truncated at the current panel width.

### 7. Missing visibility of metrics and telemetry panels

FR-009 (real-time metrics), FR-010 (agent telemetry), and FR-025 (performance
telemetry) all require visible data readouts. These are not visible in the
screenshot. If they exist elsewhere (e.g., an overlay on the viewport), this is
fine — but if they are absent from the UI entirely, they need to be added.

**Note:** This may already be implemented outside the control panel; verify before
acting.

---

## Recommended priority order

1. Fix truncated labels (highest user-facing impact, likely a width/layout tweak)
2. Clarify "Agent ID" / "Select by ID" button names
3. Clean up Export section hints and path display
4. Add units/range context to sliders
5. Fix numeric precision inconsistency
6. Label algorithm/dimension dropdowns clearly
7. Verify metrics/telemetry visibility