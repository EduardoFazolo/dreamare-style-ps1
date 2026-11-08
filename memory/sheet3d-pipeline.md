---
name: sheet3d-pipeline
description: APPROVED 2026-10-26 ("YES YES YES"): tools/sheet3d builds PS2-era 3D characters from a spec: AI model sheet (front, side, back) -> carved hull -> Blender low-poly + UV -> projection bake -> GLB
metadata:
  type: project
---

SUPERSEDED 2026-10-29 by [[ps1-character-look]] (ps1char, itself deprecated 2026-11-08 for ps1BodyV3, tools/ps1bodyv3) for new people; sheet3d is kept only for characters already built with it.

The user's breakthrough character method (2026-10-26). The RE4 apron woman was first built by hand in art/re-villager/; the user then asked for a fully programmatic version that works for any aesthetic, body type or person.

**Run:** `python3 tools/sheet3d/sheet3d.py tools/sheet3d/specs/<id>.json [--only stage | --from stage]`. Output goes to out/sheet3d/<id>/ and public/env/<out>.glb.

**Spec fields:** aesthetic, person, body, outfit, height, seed, tris (~3000), texture (512). front/side/back can point at existing pictures.

**Stages:**
1. **front:** `ai image --n 1`, orthographic A-pose on a flat grey backdrop.
2. **side, back:** `ai edit` of the front, one job each.
3. **depth:** MoGe on the front and back views.
4. **hull:** a voxel carve: inside the front and both side outlines, and between the front and back depth surfaces (rescaled row by row onto the side outline), then marching cubes.
5. **model:** Blender decimates to the triangle budget and unwraps into one texture sheet.
6. **bake:** each texel takes the colour of the views that face it, with a depth buffer per view; texels no view sees are filled from their neighbours.
7. **glb:** Blender writes the GLB.

**Place in a scene:** `{ kind: "model", src: "re/x.glb", engine: true }`. `engine: true` swaps in oldMaterial, so the character is lit and fogged like the scene (without it, the GLB renders black).

**Built so far:** re/apron-woman.glb and re/farmhand.glb (the heavy-set farmhand was made from a spec alone and came out convincing).

**Rules:**
- **ONE generation at a time,** never `--n 4` ([[one-heavy-job]]).
- **AI only helps:** it draws the sheet; the 3D shape and the texture sheet are built from it.

**Known gaps:**
- Klein's back view can print front-only clothing (an apron) on the back.
- No rig yet: the characters can't animate or hold tools.
- Fine shirt areas bake patchy where only the sides see them (the farmhand: 59% seen).

Research: docs/research/resident-evil/how-they-were-made.md. Related: [[clothes-pipeline]], [[character-engine-v2]].

**2026-10-26, later:**
- **rig stage:** joints come from the outlines; our 52-bone skeleton is skinned with Blender bone heat into public/characters/<id>.glb plus index.json, so the result is an actor `charId: "file:<id>"` that can pose, walk, look at the camera and hold items.
- **unwrap replaced:** Blender smart-UV is gone; sheet3d.py now does its own projection unwrap, giving each triangle to the best-seeing view's chart (front and back biased 1.8). That fixed the faces smeared into sliver islands.
- **smoother hull:** gaussian 1.3 plus a smooth modifier before decimation.
- **bake:** facing^8.
- **texture:** 1024.
- **spec "from":** turns an existing design picture into the front view; "views_note" adds things the front can't show (a shell on the back).

**2026-10-26, faces and poses:** the user liked the models but said a video wasn't up to standard: the characters need different positions, poses and expressions, and smiles must come from OUR ENGINE, not from AI.

**Stage landmarks:** tools/sheet3d/landmarks.mjs runs the engine's own MediaPipe on the front view's head crop.

**Model:** the body is decimated to budget, then the face triangles are subdivided twice and shrinkwrapped onto the dense hull. Protecting the face during decimation starved the legs.

**Rig, face shapes:** the rig gets 12 face shape keys built from landmark pulls (SHAPES in sheet3d.py: mouthSmile, mouthWide, jawOpen, eyeWide, blinks, brows, sneers), so pose.expression and pose.face work. Smile pulls: corners up and back, cheeks and lower lids up.

**Rig, arm weights:** each arm bone keeps a vertex only inside a capsule round the bone and not inward of the arm. Bone heat had tied the apron to the hands.

**Gotchas:**
- Blender keeps the OBJ's frame on the vertices and puts the axis turn on the object.
- Carve pits (an apron's folds read as deep) make inward-facing walls. The character shader culls them and they show as see-through holes, while the double-sided static model shows a dark pit. Fixed with a closing plus fill-holes below the neck, depth relief damped 0.6 and capped at 0.3 of the body's depth, and the unwrap turning each seen triangle toward its view.
- Test scenes with hills: put cameras at {at, offset} heights above the ground.

**Arms:** sheets now use a wide A-pose (45°, a gap at the armpits). Arms drawn close to the body fused with the torso and dragged flaps when posed. The joint finder traces each arm to the outline point farthest from the shoulder, and the legs come from the outline at shin height. Existing characters were re-sheeted from their old front (spec "from": out/sheet3d/<id>/design.jpg). The old views are in out/sheet3d/old-apose/.

**2026-10-26, arms rebuilt:**
- **The carve runs on body_view outlines**, with the arm runs removed below the shoulders and the upper arm clipped at the body line down to the armpit. Arms come from arm_tubes, lofted along the joints with their width measured off the front picture, and Blender joins them after decimation.
- **figure_mask** seals edge leaks (closing ×6) before fill_holes; cream aprons near the grey backdrop read as holes.
- **Armpit:** the first row going down from the neck that splits into three runs.
- **Arm texture:** arm triangles take only the front or back chart, by which way they face, and are never flipped.
- **Rig:** the arm trim keeps a capsule test only (radii 0.11, 0.10, 0.10).
- **Result:** poses (stand, crouch, reach, walk clip, kneel, arms-up) and engine expressions (smile, manicGrin, worried, stunned) work on all three humans.
- **Not fixed yet:** the kneel preset pushes legs through the skirt; the farmhand's crouch hides the pitchfork.

**2026-10-26 USER CORRECTION: "the whole point of making the characters 3d was to not use AI for them."** To fix the arms, I regenerated every character's front, side and back views with AI (12 new images). That swapped the approved designs for new AI ones, and the user said everything got worse. Rule: once a character exists in 3D, poses, expressions and fixes come ONLY from the engine (rig, face shapes, geometry). Never regenerate its pictures. AI is used once to make the reference sheet, and only with permission. The original views are saved in out/sheet3d/old-apose/<id>/.
- **Restored 2026-10-26** from out/sheet3d/old-apose; MoGe depth was re-run on the same pictures, and no new images were made. Arm tubes are now opt-in (spec "arms": "tubes", only for sheets drawn with gaps under the arms). Open problem: on the restored sheets the arms are carved fused to the body, so poses that move the arms (reach, walk, arms-up) drag flaps of the jacket. Hanging-arm poses and all expressions are fine.
- **2026-10-26 ROLLBACK:** the user said every later change made the models worse ("worse than what we had before"). I restored the GLBs and tools/sheet3d code exactly as they were in an earlier video (lupe checkpoint 01a179a7, through `lupe restore <full id> --workspace /tmp/lupews`; `lupe cat` corrupts binaries). The later experiments are in out/sheet3d/backup-after-faces/. Rule: make changes to these models only as add-ons to the approved meshes, never by rebuilding them; before claiming an improvement, compare it side by side with the approved version.
- **Face controls ADDED to the approved files:** tools/sheet3d/blender_addface.py takes the approved GLB (a copy is in out/sheet3d/approved/), splits the face triangles flat in place, and adds 12 shape keys from the landmarks (out/sheet3d/<id>/face.json). The mesh, texture and skeleton are unchanged; the no-expression frame is identical to the approved one. Smile and grin work. Worried shows a thin forehead line, and the old man's smile is weak under the cap and beard.
- **Mouth bag, 2026-10-26 (user: "add 3d with the mouth bag technique... very expressive, open mouth and teeth of all types"):** blender_addface.py runs on the approved GLB.
  - **Weld:** the file has three vertices per triangle, so weld them first (remove_doubles).
  - **Split:** split the face patch, and split the mouth area once more.
  - **Cut:** an edge-path cut along the lip line, snapped to it and split; the corners stay joined.
  - **Bag:** the creator's mouth-bag loft. Its rim is the cut, it narrows back and is capped.
  - **Teeth and tongue:** teeth strips (MASK alpha through a Round node) and a tongue, with the lower teeth and tongue on the jaw.
  - **Shapes:** jawOpen is a real hinge rotation; teethBare is added.
  - **Textures:** tools/sheet3d/teeth.py paints normal, yellow, rotten, sharp, gap, gold and dentures.
  - **Result:** screams and laughs read well on the woman and the old man. The farmhand's grin tears at the chin, and manicGrin on the woman makes a V.
