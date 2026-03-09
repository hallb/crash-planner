# Retrospective: M-7 3D mode

**Milestone:** M-7
**Status:** In progress

---

## Observations

_Capture observations here throughout the milestone. Promote actionable items to retro issues when ready._

### What worked well

### Friction / what didn't work

- The 3D rendering spike (ISS-50) was a paper analysis — no code was run on the target platform (WSL2/EGL). A platform-specific ModernGL bug (`depth_func` setter crashing under EGL) was only discovered after full implementation, requiring a debugging round-trip to isolate and remove one redundant line.

### Process observations

### Ideas for rules or skills

- We should update the rules/skills to make sure that "in progress" issue updates are committed as soon as the issue is marked in progress.
- Platform-integration spikes should include a minimal runnable proof-of-concept executed on the actual target environment, even if the code is discarded afterward. The spike definition of done should include "prescribed approach smoke-tested on target platform."

---

## Promoted items

Items from the observations above that became actionable `retro` issues.

| Issue | Observation | Status |
|-------|-------------|--------|
