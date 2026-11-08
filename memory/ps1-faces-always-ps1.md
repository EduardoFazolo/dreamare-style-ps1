---
name: ps1-faces-always-ps1
description: "RULE 11-07: any face-mapping change keeps the PS1 texture look (few colours, chunky texels); 3D shape is not a reason to drop it"
metadata:
  node_type: memory
  type: feedback
  originSessionId: a2948577-a6e6-421e-ab17-f3ebbe937b41
  modified: 2026-11-07T22:27:21.434Z
---

When the PS1 head was rebuilt with the --facemap 3D mapping, the face shipped as a smooth photo texture, and the user objected: "I want them in 3d but in ps1 style, OBVIOUSLY".

**Why:** the PS1 look is the project's identity; better 3D is on top of it, never instead of it.

**How to apply:** every face texture goes through the PS1 pass. Since 2026-11-07 `ps1char.py --faces` (and so `ps1.py faces`) runs posterface.py itself at 16 colours, 128 px (`--no-poster` skips it), so this happens without a step. facelife.py (24 colours at 80 px, blink/talk frames) was rejected ("this is awful") and soft-deleted. Check close renders for PS1 texels before showing. Related: [[ps1-face-poster-then-pixel]], [[ps1-character-look]].
