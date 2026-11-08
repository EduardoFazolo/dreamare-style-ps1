---
name: slide-character-recipe
description: "how to build slide characters the user accepts — PS2 body + photo-sculpted head, generated faces, photo garments, varied poses"
metadata:
  node_type: memory
  type: feedback
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-07T00:22:29.036Z
---

2026-10-06 the user rejected the cast for three reasons:
- everyone stood in the same pose
- the outfits were "cartoon-esque lowpoly slop": the sculpted body's painted clothes
- every face looked like "the same face with a different texture": the PS2 template head

They pointed to the sculpted photo faces (two earlier characters) as the ones that work.

The recipe that fixed it (scratchpad build.mjs drives window.__app and PUTs to /__character):
- bodyGen 'ps2' + headGen 'photo', with garmentTex photo variants (public/ps2body/variants/fs-* and zz-*-photo, made by tools/comfy/ps2tex.py garment)
- face grade near neutral (sat .85, contrast 1, shadowAmt .08, highAmt .05, sharpen .4, flush .05). The defaults stack with the scene's fry and burn faces orange-red
- strong per-character mutations (nose, noseLen, eyes, eyeSpread, grin ≤1.4, chin, long, earSize, headScale 1.2–1.45); keep neckLen ≤0.7 or the head floats off the neck
- new faces generated with tools/comfy/gen.py (public/faces/gen01–14). Pad the photos so the head has room around it, otherwise the photo hair finds nothing; light hair needs a dark backdrop
- every crowd member gets a different pose: look, away, kneel, hands over the face, point, bow, arms-up, T-pose, twitch, lying down

**Why:** Elliot's people read as individuals with one wrong feature, dressed in real-looking cloth.
**How to apply:** follow this recipe for every new cast. Related: [[ps2-photo-textures]], [[ps2-body-research]]

2026-10-06 later the same day: the user rejected everything this recipe made ("10x worse", "not creepy, ominous or interesting", "BORINGGG"). Realistic people in photo clothes with mild face tweaks are the wrong direction. The closest they've seen is one of those sculpted photo faces:
- one bold dark silhouette (a hood/robe)
- a real photo face with a grotesque toothy grin, purple and pale, floating in the dark like a mask

Elliot's designs are creatures and objects with real faces (ice cream, polygons, a pigeon-headed man, skull monks, a beaked thing, a blob body), not dressed humans. Stop iterating sliders on normal faces; ask before another long build.

The neck (PS2 body + photo head), fixed 2026-10-06 after the user had fought it for 3 days. Root cause: ps2body.js picked the cut rim by height, but the cut is slanted, so it got only the front half of the opening. The seam ring sat forward and poked out through the shirt, and the back of the opening was a hole. Now the rim is the true boundary loop (edges used by one kept face), and the neck is a loft:
- bottom: the body's rim, following its slant
- top: the head's real underside (NECK.under, measured in main.js from the hull: chin 152, jaw 172/397, ears 234/454, furthest-back point)
- shape: the user's Σ sketch (straight back, front pinched at the throat), weights chest → neck → head
Debug necks by dumping numbers (rim and ring extents), not by eyeballing renders.

2026-10-06 APPROVED "slim man" archetype (the user: "I'm satisfied with this... that's kind of for the slim man archetype", one archetype, NOT the base for everyone, docs/first-slides/slope2-box1.jpg, a G-Man / Elliot TV-man suit):
bodyGen 'ps2', headGen 'photo', outfit 'suit', shoulderW 3.4, girth 1.15, armLen 1.15, legLen 1.15, headScale 1.1, shoulderDrop 0.25, boxJacket 1, pose 'rest' (arms in, palms to the thighs), skinTex 'face' + skinScale 2 (plain hands).
New params, all built this session: shoulderDrop (body.js), boxJacket (ps2body.js, thickens the top garment into a block), rest pose palms/tuck, plainHands in the skin bake. The neck test is tools/tests/neck.mjs (run it after any neck, collar or body change).
