---
name: close-face-mush
description: "why photoObject faces turn to unrecognisable mush in close shots, and the measured fix (2026-10-22 close-up video)"
metadata:
  node_type: memory
  type: project
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-22T18:15:42.355Z
---

On 2026-10-22 the user said the faces in a close-up video were "unrecognizable". There were three causes, and each was found by rendering with that one thing changed:

1. **Too small a source image.** The MJ image wasn't upscaled (1456×816, faces about 45 px). Ask the user for the MJ Upscale (Subtle) version.
2. **`terrain.retro.chars.size` 320.** Every character texture was shrunk to 320 px, then stretched across a close shot. Use 1000 for close-ups.
3. **The full old-nostalgic `terrain.finish`.** Its sharpen ×2.1, sat ×1.5 and 6 px bleed clipped the already-saturated MJ faces. Rendered with `finish: {on: false}`, the face was perfect. The gentle version that keeps the look: `{sharp 1.0, sat 1.15, bleed 2, lines 30, grain 16}`.

Also used:
- `flatShade` 0.9 on photoObjects, so the scene light doesn't carve the relief.
- `light` 1.5–1.9 on a lead whose face sits in shade (night, or a hat).

**How to apply:** for any close-up character slide, check a full-res face crop with the finish off against the finish on before export. See [[old-nostalgic-look]].

**Gotchas:**
- The zsh `set -- $s` loop doesn't split words, so the "renders" silently reused old files.
- The macOS filesystem is case-insensitive: `rm zz-ff-softA.json` also deleted `zz-ff-softa.json`.
