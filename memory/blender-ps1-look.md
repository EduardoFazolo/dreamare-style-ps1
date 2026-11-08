---
name: blender-ps1-look
description: "SUPERSEDED 2026-11-02: user wants videos in OUR engine (§9 method), never Blender; was the 10-31 Blender PS1 look test"
metadata:
  type: feedback
---

After "doesn't look nearly as good as the guys I sent" (orphanfunkhouser/ember.lite/en4ria are Blender), a Blender Eevee test (tools/blender/almost_home_room.py) was "definitely better" but "not PS1 enough". Of three treatments the user chose **#2**: render in Eevee with real lights/bloom, textures shrunk to 64 px (`PS1_TEX=64`, Closest), vertex jitter (`PS1_SNAP=0.05`: simple-subdivide then snap to a 5 cm grid), no room volume (`PS1_FOG=1`), then `tools/blender/ps1post.py <in> <out> --low 240` (point-sample down to 240 px wide, 4x4 ordered dither to 5 bits/channel, nearest upscale to 1080). Rejected: clean Blender (too modern), flat hard PS1 light (lost the mood).
Gotchas: Eevee with 1 sample turns shadows/volumes to noise: render clean at full res and downsample in post instead. Blender 5 compositor = `scene.compositing_node_group` (node group with an output socket), not `scene.node_tree`.
**How to apply:** for videos in this style, build places in Blender (bpy scripts under tools/blender/), render, then ps1post.
