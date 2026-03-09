---
id: ISS-36
title: Generate milestone/issue status reports with Mermaid Gantt charts
type: feature
status: Done
priority: null
labels:
  - documentation
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
createdAt: 2026-03-09T01:15:03.259Z
updatedAt: 2026-03-09T03:17:50.427Z
---

## Motivation

As milestones grow in number, it becomes harder to get a quick read on overall project health, what is done, what is in flight, and what remains. A structured status report would serve both team coordination and stakeholder visibility.

## Proposed scope

- Summary table: milestones with status, issue counts (total / done / remaining), bug counts (found / fixed)
- Per-milestone issue list with status and optional effort estimate
- Mermaid Gantt chart showing milestone and issue order and status
- Effort estimates on Issues and Milestones to support burn-down view

## Delivery options

- Script or skill that queries `mdp` CLI and emits a markdown report
- Could be a new skill (e.g. `generate-status-report`) or an extension to an existing one

## Acceptance criteria

- [ ] Report covers all milestones: status, issue count breakdown, bug count breakdown.
- [ ] Report includes a Mermaid Gantt chart reflecting milestone/issue order and current status.
- [ ] Effort estimates on issues and milestones are surfaced when present.
- [ ] Output is valid markdown renderable in the IDE.