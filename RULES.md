# PS1 / PS2 nostalgic (style)

How scenes in this style look. Only for projects and scenes that use it (`node tools/style.ts list`); another style's scenes follow their own rules. The engine's rules (sizes, physics, layout, real light sources, composition) hold here too.

## The frame

- Late PS1 / early PS2: a low-res frame (`terrain.res`, 240 by default), a crisp full-res final frame, blocky nearest-filtered low-res texels on surfaces (the Silent Hill look), 15-bit dither when there's no finish.
- The old nostalgic finish (`terrain.finish`, `src/scenario/finish.js`) when the ask is Nintendo / PS1 / PS2 era. A scene with a finish is judged at `--width 1080` and only shrunk afterwards.
- No affine floor warp unless the scene asks for the PS1 swim (`terrain.wobble`).
- One post filter across a whole multi-place video.

## Surfaces

- Every surface is a `designTex` on a CC0 photo, read as nearest low-res texels: never a flat colour, never bricks drawn in code, never a photo washed with one colour.
- "More colour" means dirty, many-hued textures, not coloured lights. Don't calm or fade wall textures.

## Characters

- New people and creatures are ps1char: read `CHARACTERS.md` before making or editing any body or face.
- Faces keep the PS1 texture look (few colours, chunky texels) whatever else changes: colours first, then pixels.
