---
name: photo-hair
description: Hair must come from each face's own photo (Dreamland realism), never invented sculpted styles
metadata:
  type: project
---

2026-09-28: the user said the sculpted hairstyles (short/bowl/afro/mohawk… shells with a tiled 64px hair patch) were "silly" and removed the creepiness. Dreamland's heads are unsettling because the real photo, hair included, covers crude geometry. Built `src/photohair.js` (hairStyle 'photo', now the default and always picked by randomize): a shell over the head hull whose hair start and thickness per outline direction come from the segmenter mask, textured by the photo crop (non-hair filled from the nearest hair) with 1:1 ping-pong UVs. The user's rules: each face keeps its own hair; without photo hair, go bald or balding; under mutations the hair hugs the face but never enters it.

The user confirmed the first version: "non ironically actually much better".

**Why:** realism of the photo texture is what makes it creepy; the same lesson as [[head-texture-approach]] and [[dreamland-texture-first]].
**How to apply:** improve hair by measuring the photo, not by adding invented styles. Judge on front, side and back renders (the scratchpad ph.mjs harness renders faces × 3 views). The user didn't want a pre-measurement of the face set: "I want the solution to just work."

Follow-ups done the same day:
- **Cheek "commas" on the side of the head:** measured as hull mirror lines crossing hair locks in the face texture. The fix: shorten each line before the first hair texel (mask or <0.5× skin brightness), with neighbours agreeing. Skipping past the hair, or switching anchors, made it worse.
- **Long hair:** a curtain hangs from under the shell when the photo shows hair below the chin.

2026-10-07: generated source faces must be on a LIGHT plain background with the whole head of hair in frame. Dark hair on black backdrops cut out as a thin strip and every character read bald (the user: "THEY ARE ALL BALD"). Don't hack the hair code (a hairFull override was tried and was the wrong way); fix the photo. Expressions belong in the photo too (open mouths need openMouthLayout in main.js, already built), never in strong mouth morphs, which tore lips.
