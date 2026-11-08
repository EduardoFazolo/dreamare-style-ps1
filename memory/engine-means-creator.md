---
name: engine-means-creator
description: "our engine" / "engine characters" = today ps1BodyV3 (tools/ps1bodyv3, v3- ids); ps1char deprecated 2026-11-08, the old creator 2026-11-07
metadata:
  type: feedback
---

On 2026-10-25 "our engine characters" meant the old character creator (roll/build), and building new v2 photo-head masks
instead got "wtf did you do this whole time". On 2026-11-07 the user asked to deprecate that creator "once and for all so
agents stop using it by accident": it moved to `deprecated/creator/` and `roll`/`build` print a warning.

**Why:** the lesson still holds (use the established character path, don't invent parallel tech), but the established
path is now ps1BodyV3: on 2026-11-08 the user deprecated ps1char ("v3 feels better already").
**How to apply:** read `CHARACTERS.md` (repo root) before any body or face work; new people and creatures are
`tools/ps1bodyv3/ps1.py gen/make <image> v3-<id>`. The old ps1char is in deprecated/ps1char and refuses new ids. Use the old creator only to rebuild a character already made with it. See
[[creator-deprecated]].
