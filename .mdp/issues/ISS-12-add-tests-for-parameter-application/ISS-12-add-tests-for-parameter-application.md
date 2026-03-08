---
id: ISS-12
title: Add tests for parameter application
type: task
status: Backlog
priority: null
labels: []
assignee: null
milestone: M-2
estimate: null
spent: null
dueDate: null
blockedBy:
  - ISS-9
parent: null
relatedTo: []
checklist: []
log: []
createdAt: 2026-03-08T02:05:00.000Z
updatedAt: 2026-03-08T02:05:00.000Z
---

## Description

Unit tests: param change takes effect within one step; agent_count change reinitializes state arrays; invalid values produce error (NFR-005). Stability tests: simulation runs 10+ steps without crash at agent_count=10 and agent_count=500 (NFR-003). NFR-014: parameter application testable. Per 10-testing-strategy.
