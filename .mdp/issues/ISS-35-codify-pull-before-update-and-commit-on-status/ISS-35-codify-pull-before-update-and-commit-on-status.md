---
id: ISS-35
title: Codify pull-before-update and commit-on-status-change in execute-milestone skill
type: task
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
createdAt: 2026-03-09T01:11:38.329Z
updatedAt: 2026-03-09T01:12:05.591Z
---

## Observation (from M-3 retro)

Issue files were updated in batches at the end of the milestone rather than at each status transition. This leaves planning state invisible to the team during execution, and risks merge conflicts when multiple contributors update issue files concurrently.

## Required change

Update the `execute-milestone` skill to include an explicit micro-workflow at every issue status transition:

```
git pull
mdp issue update <id> --status <new-status>
git add .mdp/issues/<issue-dir>/
git commit -m "chore(plan): <ISS-id> status → <new-status>"
git push
```

This applies at minimum to the following transitions:
- Backlog → In Progress (when starting an issue)
- In Progress → Done (when completing an issue)

## Acceptance criteria

- [ ] execute-milestone skill documents the pull-before-update step explicitly.
- [ ] execute-milestone skill documents the commit+push-after-status-change step explicitly.
- [ ] The pattern is visible as a named step or checklist item, not buried in prose.