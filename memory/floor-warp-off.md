---
name: floor-warp-off
description: 2026-11-03 "floors move or stretch" = affine texture warp; off unless terrain.wobble; retro copies keep mipmaps
metadata:
  type: feedback
---
Floors that "keep moving or stretching" were the PS1 affine texture warp: the same deck boards curved and changed angle after a 1.2 m camera move at affine .5, and stayed straight at 0. `src/editor/main.js` now sets affine only when `terrain.wobble` is on; a scene's `affine` alone does nothing.

**Why:** the user called it a bug across the whole engine; it isn't a look they want. Retro copies also lost mipmaps, so far floors crawled; they now keep nearest up close and mipmaps far off (power-of-two, no alpha).

**How to apply:** never bring the warp back as a default. Test floor bugs with visible straight lines (boards) and a real camera move: frame-difference numbers were swamped by grain and told nothing. See [[ps1-silent-hill-texels]].
