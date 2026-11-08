---
name: ps1-face-poster-then-pixel
description: "2026-11-05 user picked 16 colours THEN 128 px for faces as closer to PS1; order is colours first, each block keeps its most common colour, 64 px breaks the eyes"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 29684491-b559-4066-b448-b8fafd3b1d5f
  modified: 2026-11-05T20:08:01.697Z
---

Faces read as PS1 when the colours are cut first (16, one palette per character) and only then pixelated to 128 px, with each block taking its most common colour rather than an average. User, looking at that version: "this made this version looks closer to ps1". They proposed the order themselves ("posterization first to adjust the colors, then pixelization").

**Why:** faces were swapped in with 6,000-27,000 colours and half the ad cast at 256 px, finer than the 240 px game frame, so they read as smooth photos on a blocky body. The picked picture also had `fx.crisp` and real light on. 32 colours looked the same as before; 64 px turned eyes into blobs.

**How to apply:** since 2026-11-07 it's the default for every ps1 character (the user asked for faces in PS1 style on 11-07): `ps1char.py --faces` ends with it. Older characters only change when rebuilt or run by hand. See [[ps1-character-look]].
