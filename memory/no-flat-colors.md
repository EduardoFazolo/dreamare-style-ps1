---
name: no-flat-colors
description: "RULE: never flat-coloured low-poly surfaces; every surface (walls, windows, doors, trims, props) gets a real texture"
metadata:
  node_type: memory
  type: feedback
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-21T00:19:27.850Z
---

Never ship flat colours on geometry again: no plain-colour windows, doors, beams, boxes, plates. Every surface wears a real texture (weathered wood with visible boards, glass with panes and glow, door planks, stone, shingles), at a believable scale, with contrast; never greyed-out or washed so it reads flat.

Sources: simple tiling textures -> generate with ComfyUI (`ai texture tile` / `ai image`); complex ones -> give the user a Midjourney prompt ([[midjourney-budget]]).

**Why:** 2026-10-20 shack alley: walls were desaturated, posterized tiny-scale planks + flat orange windows; user: "USE THE FUCKING WOOD TEXTURES ... No more fucking low poly flat colors, this is a fucking rule."

**Second offence 2026-11-02 (rs-laundry):** a Kenney toy sedan (palette swatches, no real texture) parked in an otherwise designTex scene; the user was furious ("how many times do I have to tell you"). Imported models count: Kenney cars/furniture are banned in shown places (check.mjs now warns); use env/psx-cars (GGBot CC0 PS1 cars, painted 128 px) or build from designTex. Render every prop close before showing; a gate "blob/no detail" flag = fail.

**How to apply:** before showing any built place, check every material has a map; compare against the reference's texture density.
