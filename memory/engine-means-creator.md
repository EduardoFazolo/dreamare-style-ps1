---
name: engine-means-creator
description: "our engine" / "engine characters" = today the ps1char cast; the old creator (roll/build) was deprecated by the user 2026-11-07
metadata:
  type: feedback
---

On 2026-10-25 "our engine characters" meant the old character creator (roll/build), and building new v2 photo-head masks
instead got "wtf did you do this whole time". On 2026-11-07 the user asked to deprecate that creator "once and for all so
agents stop using it by accident": it moved to `deprecated/creator/` and `roll`/`build` print a warning.

**Why:** the lesson still holds (use the established character path, don't invent parallel tech), but the established
path is now ps1char.
**How to apply:** read `CHARACTERS.md` (repo root) before any body or face work; new people and creatures are
`tools/ps1char/ps1.py gen/make`. Use the old creator only to rebuild a character already made with it. See
[[creator-deprecated]].
