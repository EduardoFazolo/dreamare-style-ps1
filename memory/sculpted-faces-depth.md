---
name: sculpted-faces-depth
description: weird characters = weirdness IN the face photo (edit.py) + per-face measured depth (MoGe, geoSource 'depth'); never post-hoc hue/eyeVoid/sphere stretching
metadata:
  type: feedback
---

On 2026-10-08 the user rejected six "otherworldly" writer variants built with hue shifts, painted void eyes and sphere or cranium pushes: "you are literally just stamping a face into a random shape... I want a sculpted face so the features are all correctly 3d".

The root cause was the engine itself. geoSource 'fitted' took x/y from the photo but z from the one canonical face, so every head had the same relief.

The fix:
- **Measured depth:** tools/comfy/facedepth.py runs MoGe (MIT; ~/ComfyUI/models/geometry_estimation, run fp32 via moge_run.py in ComfyUI's venv) and writes <face>.depth.png/.json. geoSource 'depth', now the default, uses each face's own measured relief, faded to canonical at the oval edge.
- **Skull:** skullFit builds the cranium from the head's silhouette instead of an egg.
- **Weird features:** put them into the photo with tools/comfy/edit.py (FLUX klein edit): grey skin, black eyes, horseshoe hair.

Hair follows the same rule: change the photo (photo hair), not the sculpted hair styles, which read as toy wigs ([[photo-hair]]).

**Why:** the user built the character engine to sculpt real faces. Texture tricks on a generic head read as stamped.
**How to apply:** for a new weird character:
1. Edit the face photo.
2. Run facedepth.py on it.
3. Build with geoSource 'depth' and hairStyle 'photo'.
4. Check it in the creator from 0°, 45°, 90° and the back (scratchpad heads.mjs) before putting it in a scene.

Related: [[slide-character-recipe]], [[deterministic-fixes]]
