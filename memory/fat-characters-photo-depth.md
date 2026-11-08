---
name: fat-characters-photo-depth
description: "very fat / Jabba characters = one full-body photo + MoGe depth relief (photoObject \"depth\"), never a fattened human body"
metadata:
  node_type: memory
  type: feedback
  originSessionId: bf78468a-e6a7-4067-9115-7767f465dc90
  modified: 2026-10-09T16:24:04.890Z
---

2026-10-09: every attempt to make the PS2 body fat failed: girth, MakeHuman's weight morph, fat pads, a belly dome,
Inflator-style bone swelling, a blob torso, a lathed "mass" with a shirt photo. The user called them weird, an egg
costume, "wtf". What finally worked ("brah... that is much better"): one generated photo of the whole fat man, made by
edit.py from his face photo (face pasted on a grey canvas, "turn this into a full-body photo of this same man…", 3 seeds),
measured with MoGe (tools/comfy/facedepth.py on the photo), cut out BY DEPTH (a colour key left shadows), and shown as a
`photoObject` with `"depth"` (front = measured relief, back = pillow). Slide 6 Pump Man: public/env/objects/pump-man.*.

**Why:** in the user's Elliot reference the face, jowls, belly and arms are one shape with one skin. Gluing a photo head
onto any fattened body can't give that; one photo of the whole person can.

**How to apply:** for extreme body types in front-facing shots, use whole-body photo + depth. Limits: no back (the side
cracks), no limb motion. Use the 90th percentile of the figure's depth as its back, not the max. The user also asked:
shirt in the body texture, rounded shapes, narrow sloped shoulders, and to try a few techniques side by side before
building one out. Related: [[sculpted-faces-depth]], [[one-model-at-a-time]], [[elliot-character-anatomy]]
