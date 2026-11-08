---
name: head-texture-approach
description: "What finally worked for the head: face-grown hull + mirror-padded face texture; what the user rejected"
metadata:
  node_type: memory
  type: project
  originSessionId: 2c83346d-a955-4794-ac5f-664806b0f03f
  modified: 2026-09-25T21:21:15.143Z
---

After many failed rounds (2026-09-25), the user called this "insanely better": the head is the ORIGINAL hull grown from the face's own outline (b18118e: 7 rings shrinking to a pole behind the head), one mesh with the face, textured only by the face's own photo texture. Past the outline the UVs mirror back INTO the face at 1:1 scale along mouth-safe rim->skin-anchor lines, bouncing between rim and anchor (headMap 'mirror', src/head.js classicBand). The face texture sits on a flat skin-tone background with 1-2% edge padding.

**Why:** the real photo texture covering the whole head carries the creepy, human feel. Every stretch/smear approach streaked on side views. The user rejected all of these: flat or synthetic skin tone ("pink guy"), a face mask on a sculpted skull, photo projection, harmonic colour fill, stretch-to-edge, and radial skirt padding.

**How to apply:** never shrink or fade the photo's coverage, never paint flat skin over the head, and never stretch texture far (streaks). Judge changes on side views and against the old commits. Related: [[dreamland-texture-first]], [[deterministic-fixes]].
