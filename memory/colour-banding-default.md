---
name: colour-banding-default
description: RULE 11-05 terrain.poster = 4 by default on new places, but a per-place choice, never a hard rule; old scenes keep their values
metadata:
  type: feedback
---

Colour banding (`terrain.poster`) is on by default at 4 for new places, and any place may use another value or 0.

**Why:** the user compared with and without on 11-05: "Yes by default, but this can be modifiable instead of a hard rule". It replaces the old "stays 0" rule.

**How to apply:** builders set it explicitly. `check` warns only when it's missing. Don't rewrite existing scenes to change it: 218 have no key and draw with no banding, and some were already uploaded.
