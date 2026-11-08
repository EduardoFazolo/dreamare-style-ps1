---
name: old-nostalgic-look
description: "old nostalgic" = approved 2026-10-19 look (smooth 3D + nearest photo textures + finish); finish defaults LIGHTENED 2026-11-02 (grain 7, lines 14, sharp .6)
metadata:
  type: feedback
---

When the user says "old nostalgic" they mean this look, most of the time (user, 2026-10-19: "THIS is the kind of shit I'm looking for"):
- Scene: terrain.smooth (anti-aliased frame upscaled smoothly, no pixel grid, no vertex wobble), CC0 photo textures (ambientCG) small with nearest texels (ground cc-*.png), photo-leaf cardTree props (src/scenario/photoprops.js), 45 deg lens, all old post filters (crt/vhs/nostalgia/tvColor/fry) off. Test scene scenes/zz3d-forest.json.
- Finish (tools/look/old-nostalgic.py, offline for now): oversharpen (amount 2.1, radius 1.0), NO large local-contrast/clarity (it drew dark outlines: rejected), saturation 1.5, NO vignette, VHS: chroma bleed 6 px, line jitter, fixed tinted scanlines every 4.5 px at 1920 with his strength (lines 52, alternating so brightness is kept), clumped 2-3 px grain (24) over everything incl. sky, speckles, head-switch band.
- Measured target: his line strength row-std ~30 on flat sky; detail (laplacian std at 540x960) ~40-45.

**Why:** the user rejected every softer/cleaner version (soft "measured" chain, pixel/Doom filters, Melvus-bright) and lost patience when noise/VHS were missing.
**How to apply:** default to this finish; judge lines/grain on 1:1 crops (shrunk previews hide 4.5 px lines). Related: [[elliot-aesthetics-v3]]

2026-10-19 applied to 8 existing places (zz-old-* scenes; old post filters off, terrain.smooth on, then tools/look/old-nostalgic.py): user "looks really cool ... in general, this is nice". Bright places hold. Dark places (a night farm, a mushroom wood) sink to black once the old filters' lift is gone: their lighting must be raised (open task). Sky option: tools/look/sky-regen.py (squeeze + 4x-UltraSharp AI upscale, sky only); user: 5 rounds is the limit. Posterizing characters (palette or per-channel levels) was tried and rejected 2026-10-19; brick-style posterized look should come baked into generated textures (Midjourney/Klein), not converted photos. Flat colours on houses/streets must be replaced by real textures (open task).
2026-10-19 now LIVE in the engine as a post stage: terrain.finish (src/scenario/finish.js, last pass at output size in stage.js render). Off unless set; "finish": {} = the approved look; knobs sharp, sharpR, sat, bleed, jitter, lines, linePeriod, grain, grainSize, speckle, headSwitch, fps (0 drops a part; on:false disables). Matches the offline script within ~4 levels mean, detail 26-27 vs 28. Lesson: GLSL fract(sin()) hash breaks on large pixel coords (returned 0: dark grain, specks everywhere): use Hoskins sin-free hash.

**2026-10-23:** the measured Elliot finish chain (docs/research/elliot-v3/tools/chain.py, run as tools/look/elliot_finish.py: crushed blacks, saturation 0.6, clarity, almost no grain) was applied to void-pick, and the user rejected it: "so much worse… the static filter and the post processings we had added more style. The colors seem disjointed now." Keep our finish (grain, lines, sharpen, bleed) as the shared look. A retention grader's "murky/grain" penalty does not override the user's taste on the finish.

**2026-11-02 defaults lightened (user: "the defaults here are making it really bad … this filter gives some magic to us … probably way less strong"):** FINISH_DEFAULTS now sharp 0.6, sat 1.15, bleed 2, jitter 0.5, lines 14, grain 7, grainSize 1.4, speckle 0.0003 (head band kept). The old strong values (above) buried signs/faces in grain on dark path-traced scenes. Keep the filter ON, but this lighter strength is the default now; the strong numbers above are history.
