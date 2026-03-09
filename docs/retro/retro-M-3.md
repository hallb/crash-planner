# Retrospective: M-3 Config persistence + pause

**Milestone:** M-3
**Status:** In progress

---

## Observations

_Capture observations here throughout the milestone. Promote actionable items to retro issues when ready._

### What worked well

- This milestone went very smoothly overall.
- The retro process provided a dedicated place to capture improvements without interrupting the main execution flow — observations could be recorded as they arose and addressed separately.

### Friction / what didn't work

### Process observations

- Issues should be updated while being worked on during a phase. We should be able to tell to do, doing, ready for testing, done as we go. Also, issues should probably be committed (and pushed if there's a remote) ASAP since they're meant for coordination with the rest of the team.

### Ideas for rules or skills

- Create a way of generating a status report on Milestones, Issues, Bugs found, Bugs fixed, and work remaining. We might want to put effort estimates on Issues and Milestones. We might want to use Mermaid to draw Gantt charts to show status, and to reflect the order of implementation for Milestones/Issues.
- Consider updating our phase execution rules/skills to make commits happen after each issue is done. A pre-condition for committing would be making sure the cibuild passes locally, unit tests for the issue are complete and passing and have been mutmut tested.
- The issue status / commit-early observation above is a good candidate for a rule or skill update at closeout — likely a refinement to the execute-milestone skill and/or the phase execution rules.
- Commit the issue file whenever its status changes (e.g. Backlog → In Progress → Done), not just at end-of-milestone. This keeps planning state visible to the team in real time.
- Pull and checkout the planning repo immediately before making any MDP updates, to avoid merge conflicts when multiple team members are committing issue files concurrently.
- Potentially update the save/load config to provide a filename, so we can store multiple configs.

---

## Promoted items

Items from the observations above that became actionable `retro` issues.

| Issue | Observation | Status |
|-------|-------------|--------|
| ISS-34 | Support named config files for multiple saved configurations | Backlog |
| ISS-35 | Codify pull-before-update and commit-on-status-change in execute-milestone skill | Done |
| ISS-36 | Generate milestone/issue status reports with Mermaid Gantt charts | Backlog |
