---
name: ps1-cast-build-rules
description: "RULE: ps1 cast = arms-clear A-pose photo + photo-SHELL body (segments rejected 11-02 as 'ugly squares') + clips only; check skeleton overlay + 4 angles"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 8a167cb6-032e-4445-9cbf-b3ad63a760f4
  modified: 2026-11-02T22:53:28.513Z
---

On 2026-11-01 the out-of-fuel clerk was built as a plain photo shell. His arms were fused to the body, and he stood on the `stand` preset. The user saw it from the side and was furious: "you threw a PNG on top of the body", the chest folded in, and the head turned alone.

**Why:** a photo-shell body tears in any pose away from the A-pose. Arms that touch the torso in the photo get welded to the chest by bone heat. The approved fix (segments.py, 2026-10-31) already existed and I skipped it. See [[ps1-character-look]].

**How to apply:** for every ps1 person:
1. **Source photo:** arms clear of the body all the way down. Use an arms-clear A-pose reference photo as the `--refs` pose reference. Get a clean cut through a Klein "background to flat chroma green" edit, then key the green.
2. **Body:** the photo shell, `ps1char.py <cut> <id> ...` with no PS1_BODY. Then run `ps1char.py <cut> <id> --faces`. Segments (`PS1_BODY=segments`) only if the user asks for them; see the 11-02 update below.
3. **Animation:** clips only: `anim` + `pose: {clip, look, expression}`. Never the `stand` preset on a ps1 body.
4. **Check:** render front, 3/4, side and back (a zz scene) before showing anything.
5. **Look turn:** the look-at now turns Spine1/Spine2 a little (`pose.lookBody`, default 1). The user doesn't want the head turning separately from the body.

**Update 2026-11-02 (a video with children):** the user rejected the segmented body ("a bunch of ugly squares"). The photo shell (the photo-shell method, no PS1_BODY) is right *when the skeleton is right*. The shell's "arms disappear / hands fly off" and "head takes the collar" failures were joint and cut bugs, now fixed in ps1char.py:
- **Hands:** `arm_lobes` follows each arm below the elbow as its own outline lobe. The old finder read a flared nightgown's hem as the hands, so the sleeves were bound to the legs.
- **Neck cut:** now just under the chin (chin + face/10). It used to be chin + face/3, which cut through the collar.
- **Face strands:** the edge strands are opt-in (`--face-strands`); they showed as dark bars across the cheeks.
- **Long hair hides the shoulders:** pin them with `--joints` (as for cb-lead).
- **Always check:** draw the joints over the photo (each arm chain must run down the sleeve) and count the forearm/hand vertices in the GLB (a good build has about 40-60 per bone).
- **Clips:** they pitch the head down: q-idle 13°, ninjajump-idle 34°, zombie-walk 59°. That's the same on a masked character, where the mask hides it. On children use `pose.look: 'camera'` (needs `pose.clip` set too) or a head-layer idle.
- **Round limbs (11-02, user: "give these limbs a full 3ness all around"):** shape() now sizes each part by its own local thickness: the largest inscribed disc covering the pixel, computed separately for the arms (`arm_mask`: outside the torso's run, armpit width above the armpit) and the rest. The old 40 cm max-filter made arms flat fins, 16 cm deep and 6 cm wide, invisible edge-on, and its torso disc built the arm roots torso-deep, which folded into flaps under raised arms. The joints are now found before the hull, because the part split needs them.
- **Holes in the side (11-02, user: flying lead "pretty bad still"):** `free_arms` deleted the faces joining the arm to the torso, which left the torso's side open wherever the arm lay against it in the photo; it showed as a gap at the waist in the swim clips. Now each piece's front rim is zipped to its back rim (with UVs taken from the cloth a few cm inward). Don't keep the webbing faces on the body: they stand as a fin where the arm was. The leg weights also fade into Hips over 0.3·hip height below the hips, so a dress doesn't tear at a hard border. The rig log now prints `arms freed: N cut, M zipped`.
- **Robed, wide-sleeved figures (11-03, a cleric and a townswoman):** `arm_lobes` found no separate arm below the elbow, so the hands landed on the robe at hip height and the sleeves webbed down to the skirt in every clip. Fix: hand-placed `--joints tools/ps1bodyv3/joints/<id>.json` (elbow, wrist, hand tip on the glove; Right mirrors Left) plus `--body-tris 800`: at 350 the sleeve and glove got so few faces they rendered as paper fins and spikes.
- **Repose in the photo first (11-03, user idea):** `tools/ps1bodyv3/repose.py <cut> <out> --angle 22 [--joints fix]` swings each arm down round the shoulder (skinned 2D blend) and turns the hand back onto the forearm at the wrist, fills holes, writes `<out>.joints.json` and runs depth; then ps1char on the result with that joints file. Arms raised ~40°+ or hands bent out at the wrist turn into sideways claws when clips lower them; the approved cast sources are ~24-29°.
- **No see-through parts (11-03, user: "extremely important"):** the front-to-back rim zip left 8 openings on the cleric (background through the glove) and 21 three-face edges. Replaced by `close_holes` in blender_ps1.py: every opening the webbing cut leaves gets a centre vertex (averaged weights) and a triangle per open edge. The rig log prints `open edges after join: N`; it must be 0. Check a GLB with a weld-then-count script (the GLB splits every face's verts, so count after remove_doubles).
- **Mitt hands (11-03, user: hand "looks cut, doesn't connect"; "ps1/ps2 style, make it simpler"):** `ps1char.py ... --mitts` swaps the photo-shaped hand for a 32-triangle PS1 mitt (palm, fingers, thumb) starting 3 cm inside the sleeve, rigid on Hand, uv from the photo's glove. Use it whenever a glove/hand sits below a wide cuff or reads as detached.
- **DEFAULT since 11-03 (user: "use this method from now on, deterministic"):** ps1char auto-reposes (>32° arms or >35° wrist), builds 800 body tris, mitts by default (in line with the forearm, palm texels), caps every opening (0 open edges). Opt-outs: --no-repose, --photo-hands.

**No-neck / food characters (2026-11-03, a sausage character on q-dance):** the joint finder puts the spine above the neck on a body with no neck, and the head floats off. Recipe: Klein edit the cut-out on flat green ("same character, symmetrical A-pose, arms clear, remove the prop"), greenkey, ai depth, then `ps1char.py <cut> <id> --joints <hand-placed joints.json> --no-repose --photo-hands --back-skin`. Repose pinched the waist and mitts came out dark on this body. `--back-skin` (new flag) paints the back of the head in the body's colour under the hat, instead of the hat's colour. Open defect: a ledge at the neck cut and a darker head than body.
