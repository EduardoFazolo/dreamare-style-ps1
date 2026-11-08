---
name: character-engine-v2
description: 2026-10-15 user starts a character engine v2: late-PS1/early-PS2 look, outfit-as-mesh, few predictable sliders, simplified bones; fully different from v1
metadata:
  type: project
---

After posting Who Worships Mawkworth (2026-10-15) the user said the videos "lack personality" and asked for a v2 of the character engine, fully different from v1:
- copy the aesthetics of late PS1 / early PS2
- model around the clothes (the outfit is the mesh), not a body with garments layered on top
- less customisation: bodies a little customisable but predictable, not every character extremely unique
- simplified bones

Research (obscura) into how PS1/PS2 characters were made goes to docs/research/ps2-v2/report.md.

**Why:** v1's endless per-character uniqueness (MakeHuman body + baked garments + many sliders) produced characters without personality.
**How to apply:** agree the v2 spec with the user from the research before building; v1 stays as is. Related: [[ps2-body-research]], [[elliot-character-anatomy]], [[clothes-first-bias]]

Progress 2026-10-15 (src/v2: kit.js tubes + painted UV textures, outfits.js suit/reaper/butcher, head.js photo head, face.js v1 warps + grades, char.js, prop kind v2char; test scenes zz-v2fen*, zz-v2face-*):
- Outfits-as-mesh: "definitely look better" than v1.
- Era: picked PS1 (64 px face, 16 colours, half-size outfit sheets, nearest, affine + snap) over photo and PS2.
- Faces: smooth egg head = "balloons"; v1 sculpted heads transplanted onto v2 = worse ("v2 was better").
- Face methods test (out/v2-face-methods-1.jpg): user picked plain PS1 face (method 1) over sharp texture, real eyeballs, gloss, and an extreme-expression photo. Don't push the "alive eyes" theory again without new evidence.
- Era target corrected 2026-10-15: "early PS2" = the user's refs (GTA3 Claude, PS2 Matrix-game men, Bond, PS2-cover parodies): smooth airbrushed painted faces, smooth shading, solid sculpted hair, no pixels. Era 'ps2early' in kit.js (airbrush + bakeShade + smooth heads).
- Hair: my guessed procedural hair (striped beanie, chef-hat pomp, see-through fringe triangles) made the user angry ("are you mocking me"). Rebuilt from research (docs/research/ps2-v2/hair.md): solid shell, curved hairline with 0 thickness at the edge, one volume bump, flow UVs, gradient-dominant texture. Research before building anything that has a known craft.
- 2026-10-15 first v2 scene (an arcade street scene, removed 2026-10-18, builder scratchpad arcadebuild.py): user "looks pretty cool". Recipe that worked: era 'ps2early', 11 hair styles (hair.js HAIR_STYLES), one grade per character, a whole street in the same clean style (no vhs/fry), purple storm sky + lamps. Open issues: stiff identical poses (no bones yet), black empty ground, no light pools.
- Skin roughness 2026-10-15: procedural speckle/pores/veins + a screen-space bump shader = "waaaay too rough" tinfoil, rejected. Elliot-style rough = keep the photo's own wrinkles/lumps (less airbrush) + clarity (local contrast, warm-tinted creases), faint blotches only, no bump (look.rough, face.js clarity()).
- Expressions must be sliders on one neutral photo (face.js EXPRESSIONS/expr/exaggerate), never AI-generated photo per expression: "we can't mix and match faces like that".
- Body skin = the face's own skin (2026-10-15): head.js cuts a cheek patch from the processed face, kit.stampTile grows a seamless tile (random stamps, not mirror tiles: those made X patterns), head sides use wrapped UVs at the face's texel scale, neck/hands/forearms via setSkinPatch. User: "almost good enough".
- 2026-10-15 walk-home-rules deck (first v2 video, lore-creators recipe): faces level 2 = look.faceRes 128 + faceColors 48 (256 "too real"); hair textured from the person's own photo hair (stampTile) not painted gradients ("doesn't belong to the same graphics"); no spike locks; captions pos 'low' with close-ups aimed under the chin (mid captions covered faces); never stack an expression on a photo that already has it (double teeth smear).
