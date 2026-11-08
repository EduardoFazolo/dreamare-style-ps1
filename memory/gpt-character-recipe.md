---
name: gpt-character-recipe
description: 2026-10-22 new character designs now via ChatGPT images (not Midjourney: public gallery = identity leak); the 3-step follow-up chain that produced the approved snail agent
metadata:
  type: feedback
---

On 2026-10-22 the user switched character design from Midjourney to ChatGPT images. Midjourney's default public gallery could leak their identity, and GPT renders logos and text cleanly, which merch needs. Strip the metadata from GPT files before use (re-save the pixels only).

**What got to the approved snail agent** (public/env/agents/snail-agent-gpt.png, "so much better"):
1. Upload our own approved designs as references. Give the idea and the crew name, and let GPT design the uniform and logo.
2. Its first pass was smooth modern 3D with pixel textures ("too meh"). The follow-up spelled out the PS2 geometry: flat visible triangles, hard facets, mitten hands, a boxy silhouette, blurry 128 px textures with seams, flat vertex lighting, a stiff pose.
3. The next pass was "too happy, not our aesthetic", a cartoon mascot. The follow-up asked for:
   - real photographic wet skin, desaturated, no orange;
   - tiny bead eyes;
   - a real human face stretched over the head, eyes slightly too small, a dead stare, a thin too-wide tight smile;
   - a tall gaunt body in an oversized suit, sickly muted colours.

**Why:** our creepy is deadpan and slightly wrong, not grinning and cute. Big googly eyes and wide happy grins read as mascots.

**How to apply:** for new crews (merch-able uniforms with names and logos), write the step 2 and step 3 constraints into the first prompt. See [[midjourney-for-designs]].

**2026-10-22 correction: short gag prompts beat spec lists.** The user rejected the snail/owl line ("not comically weird like the tunas"). Then a friend's one-paragraph GPT prompt beat all of mine: "create a creepy PS2 style pixelated character but they have to be fat and instead of their face being on their head put it under their belly. Have them holding their belly up so we can see the face. The face should have creepily happy eyes and a wide grin. They can have pants and shoes but no shirt."
That prompt is one absurd anatomical idea, plus a pose that SHOWS the idea (an action, not standing still with props), plus a creepy-happy face, plus a one-line style. My bullet lists of polygon and texture specs made stiff catalogue renders. Write character prompts like that one: about 4 sentences, the gag first.

**2026-10-22 the winner: fish heads.** The user rejected owl, horse, goat, pig, latex-mask realism and photoreal heads. A sardine-brothers pest-control agent landed ("fishes are just so much funnier"): public/env/agents/sardine-bros.png.
Recipe:
- Everything, the head included, is crude low-poly with blurry stretched photo textures.
- The fish points straight up out of the collar, one flat side eye, its mouth stuck open.
- An ordinary work uniform with a company logo (an open sardine tin).
- A stiff pose in a hallway.
The animal has to be dumb and edible (fish), not cute or wise.

**2026-10-22 APPROVED: the snail agent** (public/env/agents/sru-agent.png). The soulless recipe applied to the snail:
- The whole snail points straight up out of the collar, the shell on its back.
- Stiff eye stalks with flat black dot eyes, no mouth, no human face.
- A black suit, an ID lanyard, a lapel pin and a briefcase, all with a spiral logo.
- Everything equally crude: low-poly with blurry textures.
The prompt is kept in this session's transcript; reuse it, changing only the animal or the uniform.

**2026-10-22 FINAL snail agent design (the user: "I love it, let's keep it"): public/env/agents/sru-snail.png.** A combination of two GPT outputs:
- the head: a glossy slimy snail head with a wide toothy human grin, eye stalks and a big spiral shell;
- the body: a black suit with the agency lanyard, pin and coffee cup, checking his wristwatch, the body ending in a wet snail foot with a slime trail, seen three-quarter.
Method: upload both images to GPT and say which part to take from which. This is the canon snail agent; sru-agent.png (no mouth) is the backup.

**2026-10-22 CANON for the void video:**
- The snail is now the red-eyed grinning version on the snail foot: public/env/agents/sru-snail.png, cut out as sru-snail-cut.png.
- The sardine is the expressionless one, a blank human face on the fish ("funny because no emotion"): shelf-life.png, cut out as shelf-life-cut.png.
- Rejected: the cream-style manic faces on the sardine, both on the front and edited into the fish's own eye and mouth.

**2026-10-22 pick-video writing (from docs/research/elliot-truman/videos.json, his real transcripts):** his biggest shares are pure pick lists:
- ice cream: 3.9M views, 10.7% shares;
- one lick: 9.1%;
- pigeons: 6.9%.
Format: one question, then 4–6 options, each a name plus a short epithet ("Six eyed Steven", "Randy the arsonist from the nest", "The guardian of the bridge nobody uses"). 13 s, about 25 words, no explanations, it ends on the list. The user found my explained/procedure scripts "boring"; don't explain in pick videos.
