---
name: ps1-silent-hill-texels
description: RULE 2026-10-27: "PS1/PS2 realistic bad textures" = crisp full-res frame + blocky nearest low-res texels; the VHS finish and low res + smooth upscale destroyed it
metadata:
  type: feedback
---

The user rejected the textures of a village scene three times ("not even close to ps1 realistic/bad textures, you are ignoring me over and over again"). The reference was a Silent Hill room screenshot. A side-by-side crop at full size showed the cause:
- **Theirs:** a clean, sharp frame with big, crisp, square texture pixels (grime photos shrunk and point-sampled), and no noise or blur.
- **Ours:** we rendered at res 600 with a smooth upscale, and the old-nostalgic VHS finish added grain, bleed, sharpening and tape lines. That melted the texels into mush.

**How to apply** (when the user wants a PS1/PS2 or Silent Hill look):
- **Frame:** terrain res 1080, affine 0, vhs 0.
- **Finish:** grain, bleed, lines, sharp and jitter all set to 0. Keep only a colour cast (the new finish.tint).
- **Textures:** terrain.retro.env {size 128, colors 64, sample 'nearest'}.
- **Stretched faces:** a texture stretched over a long or tall face must be pre-tiled to that face's aspect (moss-tall, shutter-wide). Otherwise its texels turn into streaks.
- **Check:** always compare a full-size crop against the reference before showing anything.

Related: [[colour-from-dirt]].

**Follow-up (same day):**
- **Characters:** they need the same treatment, retro.chars {size 320, colors 24, nearest}. Clean 1000 px characters read as "no posterization".
- **Camera filter:** keep a gentle one: lines ~9, grain 6 (grainSize 1), jitter .6, sharp .35, bleed 0. Zero filter was asked about ("the filters of camera?").
- **Rooms:** ambient ~.03-.04, fog 1.6-6.5 near-black, dim warm key. Bright rooms read as "no atmosphere".
- **Signs:** hang them from an iron arm with chains, off a pillar built into the wall. A free-standing pillar with boards floating beside it read as "wtf is this pole".
- **Captions:** re-run caption_spots after every reframe. The old positions sat on top of the signs.
