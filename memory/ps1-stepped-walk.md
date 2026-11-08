---
name: ps1-stepped-walk
description: 2026-11-04 research + tool for the creepy PS1 low-frame walk; actor gait.poses holds the clip on n poses per loop
metadata:
  node_type: memory
  type: reference
  originSessionId: a2948577-a6e6-421e-ab17-f3ebbe937b41
  modified: 2026-11-04T18:02:08.319Z
---

Actor `gait: { poses: n }` (src/editor/main.js clipTime) holds the clip on n poses per loop and jumps with no in-betweens. Used on the underbelly men in co-s16 (poses 16 at rate ~.25 = a jump every .3-.6 s; `wob` makes the beats uneven).

Stepping shows only if the pose change per step is big: at a slow rate, a fixed 8-12 fps step barely moves. So step by poses per loop, not by real-time fps.

What the sources say:
- Silent Hill 1 (Vatuu/silent-hill-decomp, src/bodyprog/chara/anim.c) does NOT hold frames: it lerps 8-bit rotation matrices linearly between keys, walks/actions at 10-25 keys per second. Lerped matrices aren't renormalised in Anim_BonesUpdate, so in-betweens can distort (my reading of the code, not measured).
- Tomb Raider (TRosettaStone3, mesh_construction_animation.asc): FrameRate = game ticks per stored frame, between them slerp.
- Held frames are the modern retro-horror style: 12 fps step (Godot forum: glTF export "Sampling Interpolation Fallback" = Step).
- The look also comes from hard skinning (one bone per vertex) or separate limb meshes. Not tried here: our photo shell would tear ([[ps1-cast-build-rules]]).
- Not found: Resident Evil's frame rates, Puppet Combo / Haunted PS1 practice.
