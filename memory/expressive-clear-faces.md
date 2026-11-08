---
name: expressive-clear-faces
description: creator faces must read clearly: conservative natural grades, one strong emotion each, eyes always open; recipe that worked 2026-10-25
metadata:
  type: feedback
---

User (2026-10-25, faces-fly-south): "more visual clarity, a little more conservative on colors, more expressive
emotions, eyes always open, more expressive and interesting but without destroying them". Said "overall it's going
really well" on the creator-character version.

**Why:** strong grades (hue shift, heavy shadow tint, sunken/void eyes, grime) turned faces purple and murky, and the
painted teeth plus a baked grin made every face look like the same smile.
**How to apply:**
- Grade: hue 0, sat ~1.08, contrast ~1.12, shadow/high tint ~0.18, sharpen ~1.1, grime ~0.08, socket ~0.12, no eyeVoid/eyeStare/socketDeep, asym 0.
- Emotion in two layers: build the mouth/brows to match (grin, mouth, teeth, browAngry, eyeRound) AND hold a scene
  `pose.expression` (manicGrin, scream, rage, stunned, worried...) with exaggerate 1.2-1.4.
- Eyes: `alive.blink: false`, face `eyeWide` ~0.85, eyeBlink 0; skip source photos with droopy/heavy lids.
- Backlit faces: `glowFace` ~0.3 so they read; keep film grain moderate.
- Creator rigs have only 15 face morphs (no sneerLeft/Right, teethBare): named expressions using them (disgust, rage, rictus) silently do little; build those looks from pucker/close/funnel/brow morphs.
- Faces in profile barely show expression or eye movement; put the camera toward the front for any face that must act.
- Timed acting that worked (faces-fly-south v2 slide 5): pose.keys (eased 2-2.5 s), on.look camera with lookAt/lookSecs, pose.eyesTo. Soft = slow easing, not small values.
- Test faces in a line-up scene (one close shot each) before placing them. See [[engine-means-creator]].

2026-10-26: a close-up hook face needs atlasRes 512 (64 px goes mushy close up), light mutations when the photo is already weird (strong grin/eyeRound/eyes warps made goggle eyes), and glowFace ~0.35 when backlit. Put the weirdness in the body (neckLen 2.5) and keep the face clear. Try several faces in the real shot at full res, then pick.
