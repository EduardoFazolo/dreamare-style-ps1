---
name: finish-preview-size
description: Scenes with terrain.finish must be rendered at --width 1080 and only shrunk afterwards; small renders look double-filtered
metadata:
  node_type: memory
  type: feedback
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-20T19:50:45.542Z
---

Never render a terrain.finish scene at a small --width (400/540) for previews. The finish's grain, VHS lines and sharpen are sized in output pixels, so at 400 px each grain clump is ~3x bigger and the frame looks like the filter was applied twice (shack/fog unreadable). Render at 1080, then downscale with LANCZOS for contact sheets (that matches what the editor shows: it draws ~2560 px and the browser shrinks it).

**Why:** 2026-10-20 the user saw my small renders and said "you are applying the filter twice ... in the engine it's fine" — it was the render size, not a second filter. Related: [[old-nostalgic-look]].

**How to apply:** every still / sheet of a scene with finish: `render ... --width 1080` then resize. Open question: the 1080 export itself looks heavier than the editor view on a phone at full res.
