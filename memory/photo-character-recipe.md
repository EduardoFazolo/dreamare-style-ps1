---
name: photo-character-recipe
description: 2026-10-16 the character recipe the user approved ("that's it, this is all we gotta do"): Klein full-body flash photo -> Klein edits for face/eyes/skin -> MoGe cutout + depth -> photoObject with high-res abused-colour aged pass in our 3D scene
metadata:
  type: feedback
---

After a day of failed approaches (procedural v2 heads, v1 heads on v2 bodies, AI "PS2 style" prompts with Klein, FLUX.1-dev + PS2 LoRA), the user approved the recipe we had already used for two earlier characters:
1. Klein text-to-image: "a full-body photograph of <character>, a real photograph, harsh direct flash, on a flat pure magenta background" (short prompt; the model is good at photos, bad at "PS2 style").
2. Klein edits of THAT photo for the weirdness (expression, eyes, skin), keeping person/suit/pose: one character, several faces, reusable like Elliot's one-image-per-character.
3. `ai cutout` (MoGe, depth-based; the magenta key fails on flash gradients) + `ai depth`.
4. Scene prop photoObject with depth and `aged` at res 300-360 (176 was too pixelated in close-ups), sat ~1.45, contrast ~1.3, lift 0.16 (user picked: dark suits keep their folds), edge 0.1, fall 0.05, low tint; scene sat/punch up. (contrast and lift added to agedPhoto 2026-10-16) Light faces survive the colour push; saturated red/purple faces collapse into flat colour.

5. The scene must be in the PS2 drawn look (no terrain.look 'source'): res 300-540, PS1 ground/sky images, fry/nostalgia/tape, atmo shadows+rim+spec, characters LIT by the scene (not glow). 2026-10-16 Toffeebold in the source look with glow cut-outs was called awful ("no ps2 graphics"); in source the depth relief also banded across the eyes. Crop cut-outs to the alpha bbox (and depth png/json w,h) or feet float.

6. Expressions (2026-10-16, user: "not nearly enough exaggerated" after Klein edits): photoObject "warp" = landmark liquify sliders from src/v2/face.js ({ expr: { smile 3+, wide ~2, jaw, eyeWide <=1.5, browUp }, from }) applied to photo AND depth. eyeWide past ~2 smears. Faces the finder misses (void eyes, mannequin skin) need "from": an unedited same-pose crop (tc-gogg-ref.png). Full-body photos need aged res ~600 for face close-ups.

7. 2026-10-16 user: photos beat the engine-head route (more Elliot-like) but must be editable like sculpted characters. Done: photoObject "tone" (segmenter skin/clothes/hair + landmark eyes/mouth, sculpted slider names) and warp "teeth" (painted uneven yellow tooth rows in the opened mouth, Tumbley-sun grin), "sink"/"glint" (sockets pushed back in depth + shaded). User picked natural colours (no tone) + crazy toothy grin. Warp inverse is Newton now (fixed point folded big grins). Debug the photo pipeline alone with `dreamare eval` (scratchpad dbg/run.sh), not via scene renders. Concept lesson: an ordinary old lady "isn't weird enough"; a fat bearded man disguised as a granny was.

**Why:** the PS2/game feel comes from our engine (the scene, aged pass, light, filters), the weirdness from photo edits. Asking the model to draw "PS2 style" never worked.
**How to apply:** use this for characters; don't reinvent. Related: [[fat-characters-photo-depth]], [[sculpted-faces-depth]], [[elliot-method-verified]], [[character-engine-v2]]
