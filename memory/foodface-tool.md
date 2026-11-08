---
name: foodface-tool
description: "2026-11-04 test: tools/ps1char/foodface.py makes bodiless 3D heads shaped like objects with swappable expressions and no image AI; why Midjourney faces are stranger than our Klein ones"
metadata:
  type: project
---

User: our faces "don't look as strange and interesting as midjourney's. Not even close." Side by side, the loved ones are a real photographic human face fused into an object's skin and filling it, with wet highlights, deep sockets, round lidded eyes and clenched small teeth. Klein designs came out as monster prosthetics on a normal body.

**How to apply:** for object characters use tools/ps1char/foodface.py: photo from public/faces warped by landmarks, object colour and texture, painted eyeballs. What failed on the way, by pixels: fine-detail bump looks like foil; a big `eye_r` looks googly (.235 works); pink lips look like lipstick; open mouths look clean and tongue-heavy, so pick clenched grins (mwg-grin-*, gpt01); hair on the forehead shows through, so pick bald or high-hairline faces.

**Bodiless (user, 2026-11-04: "I don't want them to have bodies. I just want them 3d and expressions"):** I built limbs first and it was wrong. foodface.py now makes the object only, with bones tucked inside it and the neck near the bottom, so the rig only serves the expression system. Each expression is a different library photo (rage fat01, scream xp04, sad sky02) mapped to the same eye and mouth places, with painted eyes (`lid`, `tilt`, `iris`).

**Test renders:** a new scene id and actor id per render or the service shows the old model with the new texture; x=-20 is the flat spot. Not tested at 2026-11-04: changing expression live in a shot, hover motion, jaw. Part of [[own-character-generator-goal]]; related [[fused-faces]], [[ps1-make-tool]].

**Geometry first (user, 2026-11-04: "the cheese is looking more like a pillow. Why not understand the geometry of the thing first?"):** never inflate an object from its outline. tools/ps1char/foodgeo.py writes it as what it is: the wedge is a prism with flat cut sides and a rind; a bun is stacked forms (head, crust, beret, nose). The front is a part with `face: true` (blender_ps1.py names its material sheetHead so expressions swap); other surfaces are their own parts. Open: noise skin doesn't read as cheese or bread, so try real CC0 photos; the face still reads as a person pasted on, not fused; crust floats off the head in side view. The bun and cheese specs were reset to au02 as neutral (open-mouth, not the clenched crescent the references have).

**2026-11-05:** moved to experimental/tools/ps1char/ (not approved).

**2026-11-07: SOFT-DELETED** (foodface.py, foodgeo.py, foodface/ specs, design3d.py) in the face-method cleanup; restore with `python3 tools/audit/softdelete.py restore foodface`. See [[face-methods-cleanup]].
