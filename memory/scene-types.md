---
name: scene-types
description: "three scene types (2026-10-09): engine scenes, photo rooms (projected photo), Y2K photo-textured outdoor = engine + flat photo sprite trees (method 1 won)"
metadata:
  node_type: memory
  type: project
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-10T02:31:41.942Z
---

On 2026-10-09 the user split scenes into three types:
1. **Engine scenes**: our own assets.
2. **Photo rooms** (no name yet): one AI photo measured by MoGe and projected onto a box (`ai room` job, projectedRoom),
   with a short push-in (0.5 to 1 m) and real 3D characters inside. Kept after the zz-r-* tests (motel, pool, hallway,
   bus waiting room); depth-mesh and kit-built rooms were rejected.
3. **Y2K photo-textured 3D** (Elliot's backgrounds; the user says it feels like RPG Maker): 7 methods were benchmarked
   (zz-y2k-*, out/y2k-methods.mp4). The user picked **method 1**: the engine's source look plus `woods` (flat photo
   sprite trees, Doom-style), the ps1-blue-3b photo sky and a grass photo ground. AI-projected, AI-repainted, colour-table
   and ffmpeg TV-filter versions lost. All rendered at about 2 ms a frame, so cost is not the deciding factor.

**Why:** the user prefers one-shot comparisons, then engineering the winner.
**How to apply:** build Y2K outdoor scenes from method 1. Note the source look caps `vhs` at 0.15 (src/editor/main.js).

Related: [[photo-look]], [[scene-references-rpg]]
