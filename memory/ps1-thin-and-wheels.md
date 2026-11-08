---
name: ps1-thin-and-wheels
description: "11-05 what fixed a car and a beach scene: painted atlas body, spin under the aliasing limit, thin things blink, details get buried by terrain"
metadata:
  type: feedback
---

The user rejected a smooth lofted car with static-looking wheels and an empty, orange beach. Asked again for attention to details.

**Why:** at 30 fps 46 rad/s is 1.5 rad a frame, so wheels alias and look still. Sub-pixel tubes and flat ribbons blink at low internal resolution with no z-fight involved. Terrain bumps up to .68 m buried every small seabed prop, so the "details" were built and invisible.

**How to apply:** cars = ~300 faceted tris plus one painted atlas (side, top, front, rear) with nearest filter and dither, spoked wheel texture, spin about 11 rad/s for 5 spokes. Measure blink with `tools/audit/flicker.py`. Use `flatGround` when small props lie on the ground. Before building a place, list the real-thing details in `tools/ad/details.json` and check each is visible in the exported frame, not just present. Related: [[built-not-parked]].
