---
name: posterize-dither-rejected
description: "2026-11-01 user rejected the 5-bit posterize + Bayer dither post (terrain.poster) — \"looks printed on a shirt\", not PS1"
metadata:
  node_type: memory
  type: feedback
  originSessionId: 29684491-b559-4066-b448-b8fafd3b1d5f
  modified: 2026-11-01T21:09:58.911Z
---

The `terrain.poster` post step (channels cut to 5 bits, a 4x4 Bayer dither on the game pixel grid) was rejected on the zz-corner street scene: "it doesn't look pixelated or like ps1, it just looks like it was printed into a shirt". The chunkier 180 px wide frame (res 240) was also rejected; res 320 (240 px wide) matched the ember.lite reference.

**Why:** a dither pattern visible across every surface reads as screen printing, not as a console frame. The reference's PS1 feel comes from low resolution plus crisp nearest-sampled textures, not from visible dither.

**How to apply:** leave `poster` at 0 by default. Never put a visible dither pattern over the whole frame. Any jitter used in shaders (for example the air march in pathtrace.js) must not show up as a checker either. Related: [[ps1-silent-hill-texels]], [[judge-visuals-by-pixels]].
