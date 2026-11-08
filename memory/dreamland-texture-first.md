---
name: dreamland-texture-first
description: Character creator goal (Dreamland-style creepy PS2 humanoids) and the texture-first approach that worked
metadata:
  node_type: memory
  type: project
  originSessionId: 2c83346d-a955-4794-ac5f-664806b0f03f
  modified: 2026-09-24T00:38:15.930Z
---

Goal: local character creator for strange, creepy, "dreamy" humanoids in the aesthetic of the Dreamland wiki (photo-real grinning faces on low-poly PS1/PS2 heads). User had repeatedly failed going geometry-first ("low poly hell, everything generic").

2026-09-23: built the MVP (then "Dream Face Lab", renamed 2026-09-24 to Dreamare Character Engine after the repo) (Vite + Three.js + MediaPipe) proving personality comes from the face texture: photo -> landmarks -> canonical-UV atlas -> UV-space warps (grin, eyes), grade, painted makeup/teeth -> crude head + PS2 shader. User was thrilled with the result ("pretty much as perfect as it could be") — texture-first approach confirmed.

**Why:** geometry-first attempts looked generic; texture-first gave the look immediately.
**How to apply:** keep geometry crude; invest in face texture sources (AI-generated weathered faces), UV-space effects, and shared canonical UV layout.
