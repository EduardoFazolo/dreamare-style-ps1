---
name: photo-look
description: Scenes too cartoonish; per-scene terrain.look switch: 'photo' (PS2 photo tiles, judged not enough) and 'source' (Garry's Mod-like lit realism)
metadata:
  type: project
---
2026-09-29: the user said all scenes look too cartoonish/cute and asked for a reality-based look "with photos of real textures, like PS2 horror games", explicitly as a SWITCH to try first, not a replacement. Built: terrain.look = 'photo' (editor Mood toggle "Photo textures"), src/scenario/photolook.js swaps drawn textures by name (kind) for CC0 ambientCG photos in public/textures/photo, re-maps UVs to real size. Drawn look stays default; the VILLAGE fingerprint stayed identical.

**Why:** creepiness comes from realism (a subtly wrong real face); the drawn blotch textures read as cartoon.
**How to apply:** new props should use named texture kinds that have a photo (facade, pale, cobble, slab, wood, paint, wall, roof, bark, rock, stone, grass, metal, leather, mud, kerb). Photos: CC0 only ([[cc0-only-assets]]); ambientCG, not the Poly Haven API (its API needs a commercial licence). The PS2 photo swap alone was 'not even close'; the user pointed to Garry's Mod, so a 'source' look was added (lit MeshStandardMaterial + 512 px normal-mapped photos, shadows, fog, res >= 640). Pending: the user's verdict on 'source'; whether to raise render res with it; photo versions for props still drawn (mushrooms, lanterns, cloth).
