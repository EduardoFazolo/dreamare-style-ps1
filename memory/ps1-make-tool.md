---
name: ps1-make-tool
description: "Built 2026-11-04: tools/ps1bodyv3/ps1.py gen/make/faces/check/sheet turns one sentence into a rigged weird PS1 character in about 50 s; Klein designs replaced Midjourney for the test cast"
metadata:
  type: project
---

tools/ps1bodyv3/ps1.py replaces hand cut-outs and hand joints; tools/README.md is the map. Test: a market scene (tools/builders/tide_market.py, src/scenario/tidekit.js) with four Klein-designed non-humans. Part of [[own-character-generator-goal]].

Measured against hand work: cut-out IoU .90 mean on 12 approved pairs (flat key plus key_hue shadow removal; the kid's hard studio shadow still fails at .62, and foot shadows on old grey backdrops); joints 4.1% of height mean error on 11 hand files. Auto angler looked as good as the hand angler on the sheet.

**Why:** user goal of no Midjourney and fewer tokens.

**How to apply:** start every new cast with `ps1.py gen` then `ps1.py make`, and open the sheet: `check` passed magenta floor shadows until key_left was added. Faces: open face.check.jpg first; a big prop beside the head fools eye finding. Don't run faces on a real character without --replace: on 2026-11-04 an early --detect-only wiped out/ps1char/<id>/faces on 7 characters (regenerated, code fixed). Klein backgrounds aren't flat: key_hue handles it. Thin parts (antennae) are stripped by default, --keep-thin keeps them.

**3D form limit (2026-11-04):** the hull is inflated from the outline and keeps only 4 cm of the depth map, so a beak or a jutting mouth is painted on, not built. Feeding it all the depth (tested, reverted) gave real form but bricked heads, stretched texture and a torn mouth. No character has a jaw: expressions are still textures. The user liked the direction ("very promising") but called the pelican "fucked" and asked if the molar's mouth moves.

**Jaw test (2026-11-04):** tools/ps1bodyv3/jaw.py on zz-molar: jaw piece on a Jaw bone slides down over a plate. Needs a new index.json version or the render service shows the cached model (`ps1char.py --faces` doesn't bump it either). Outline is hand-placed, no detector yet; user verdict pending.

**Beak test (2026-11-04):** tools/ps1bodyv3/snout.py lofts a beak from the photo's flat one, with mirrored plates over the flat one front and back. Aim it near level or a bulging chest swallows it. A rebuilt character can render stale in the service: an index version bump wasn't enough, the page needed a reload (`touch src/editor/main.js` did it). Molar emotions clip: user "creepy and weird as fuck, but I kinda like it".

**2026-11-07 (net-mender cast):** the default magenta key ate pink tights, boots, red hands and a dress hem. Re-key with `ai.py edit` "background to flat pure green" (blue when clothes are green or olive), then `make --cut`. `make --cut` keeps the old `cut.cut.json`, so copy the new cut's json over it or check reports stale key colour. When eyes or mouth are found wrong, `tools/ps1bodyv3/faces/<id>.points.json` places them by hand. A neck set too high puts the face on the collar: open the sheet's head close-up.
