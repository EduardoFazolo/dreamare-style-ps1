---
name: ps2-photo-textures
description: "2026-10-05: clothes and skin as photo textures from local ComfyUI (FLUX.2 klein 4B edit) — the fix for 'silly not creepy' bodies; tool, params, what worked and what didn't"
metadata:
  node_type: memory
  type: project
  originSessionId: 2c83346d-a955-4794-ac5f-664806b0f03f
  modified: 2026-10-05T16:37:53.838Z
---

2026-10-05: the user diagnosed the silly look as paint under a photo face ("PS2 used real photos, which gave that weird uncanny feeling, same as we do with the head") and asked for a ComfyUI workflow for PS2 clothes and skin textures. Built `tools/comfy/ps2tex.py` (ComfyUI on :8188, `comfy` alias; FLUX.2 klein 4B + qwen_3_4b + flux2-vae, 4 steps, euler, cfg 1, ReferenceLatent):
- `garment <name> "<desc>"`: the MakeHuman garment's own UV map (public/ps2body/<name>.png) is the reference; Klein repaints it as photographed cloth and **keeps the UV layout** (tie, shirt, shoes all landed right). 30–90 s per 512 px on the M3 Pro.
- `tile - "<desc>"`: flat tileable photo (skin, cloth); centre-cropped (the model frames a limb with edges), mirrored 2x2 for seams.
- Engine hooks (per character params): `garmentTex {garment: url}` (ps2body.js), `skinTex 'name'` from public/textures/skin/<name>.png + `skinScale` (bake uniform skinTile) + `skinMatch` 0..1 (how far the photo's colour is pulled to the face tone; 0.3 looked right), `fabric {top,bottom,shoes}` tile ids for the painted/boxy body (body.js).
- Verdict on the first sheet (~/Downloads/ps2-vs-boxy-photo-textures.png): PS2 body + photo garments clearly better; **boxy body with tiled photo cloth reads as static** (tile too small at 0.9 head units, no garment structure); leather/hessian tiles came out as object photos (kaleidoscope when mirrored): tile prompts must demand a flat material only.
- zz-* files in public/ps2body/variants and public/textures(/skin) are test outputs, not finals.

**Why:** photo everywhere = one consistent dirt and light across face, cloth and skin; that is the Dreamland uncanny.
**How to apply:** make clothes with `garment` mode on the PS2 body; for skin use tiles with large high-contrast features (blotches, veins) since fine pores vanish at body-atlas resolution; measure the baked atlas (`__app.sk.bodyCanvas`) when a texture change shows nothing. Related: [[dreamland-texture-first]], [[ps2-body-research]], [[deterministic-fixes]].

**2026-10-05, later:** the user wants bodies like Elliot's (coats, suits, hats, sweaters; coarse-but-round, photo cloth), not literal boxes (a box generator was built and deleted the same day). Added to the PS2 body from MakeHuman CC0 packs (suits01, shirts01, pants01, system assets; packs fetched from files.makehumancommunity.org, the files2 mirror crawls): outfits doublebreasted, redtie, dinner, fisherman, polo, parka, stripes (ps2body.js WEARS, body.js OUTFITS) and `headwear` fedora / fedoraCocked (HEADFIT scale 1.6, up 0.35, forward 0.45, measured on face 12; `p.hatFit` overrides). bake.mjs: hats get a 400-tri budget; BAKED keys now allow hyphens (the double-breasted suit was silently missing). Skipped the two community hats whose .mhclo says AGPL despite the CC0 page. Photo repaints of all ten garments are at public/ps2body/variants/zz-<name>-photo.png; sheet ~/Downloads/ps2-outfits-photo.png.

**2026-10-05, the black bands (user: "huge black lines... shit thrown together"):** the first garment prompt asked for "real creases and folds with their shadows baked in"; Klein painted each UV piece as a crumpled garment on a table with deep fold shadows, and the UV islands cut across them (black bands down the sleeves; seen by overlaying the garment's UV triangles on the map). A game texture is a FLAT SCAN: pressed flat, shadowless even light, only weave, colour, wear, seams; the mesh and the light make the folds. The flat-scan prompt is now the tool's default; seed 11 gave a convincing worn grey suit. Always overlay the UVs (uv-*.png in ~/Downloads) when a map misbehaves.
