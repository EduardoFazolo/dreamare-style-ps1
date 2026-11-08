---
name: real-photos-not-drawn
description: "RULE 2026-11-04 - never draw bricks in code or wash a photo with a flat colour; far-away masonry = real CC0 photos, oversized, posterized, with roughMasonry()"
metadata:
  node_type: memory
  type: feedback
  originSessionId: a2948577-a6e6-421e-ab17-f3ebbe937b41
  modified: 2026-11-04T04:35:13.296Z
---

Don't fake masonry with drawn rectangles or a colour veil over plaster. The user called that repetitive and cartoonish ("what the fuck is this texture"), not "ps1 rough as our pipeline does things".

**Why:** a stone photo at real size shrinks to one flat colour from far away, so the fix is a larger photo, not painted detail. Drawn courses repeat every tile and look like a cartoon.

**How to apply:** use `roughMasonry()` in `src/scenario/gothic.js`: three real photos at 30, 42 and 26 m per repeat so repeats don't line up, tinted to one mean brightness so the mix makes no patches, posterized with contrast 2.4 and `posterMax` .5 to keep joints dark without white specks. Look at a close crop and the far strip before showing. Related: [[no-flat-colors]], [[no-black-darks]].
