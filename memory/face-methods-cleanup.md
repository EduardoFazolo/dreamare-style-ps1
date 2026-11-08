---
name: face-methods-cleanup
description: 2026-11-07 face-method cleanup — what was soft-deleted, what stays as the one face path; check before building a new face tool
metadata:
  type: project
---

On 2026-11-07 the user said "we have like 3 things to edit the faces" and approved soft-deleting every face method they had rejected or never used (tarball soft-deleted/2026-11-07-195102, 141 files; 16 removed character index entries in soft-deleted/index-entries-2026-11-07.json).

**The one face path now:** `ps1.py faces` (automatic) or the Faces tab + `faces.mjs` (by hand) → `ps1char.py --faces` + faces3d.py → posterface (16 colours, 128 px, automatic). `--facemap` stays but isn't approved. jaw.py stays in experimental. segments.py stays (it's the approved body).

**Gone (restore with `softdelete.py restore <name>`):** facelife.py and its engine frame swap (rejected 11-07), paintface.py (rejected 11-07), the Heads tab + teeth/addface/heads_prep (superseded 10-29), foodface/foodgeo/design3d/genome/snout (rejected or never judged), 16 unused characters.

**Kept on purpose:** the Characters page and everything it uses (user rule: never remove it), tools/scripts/face-landmarks.mjs (reads the creator's face library, not a copy of sheet3d/landmarks.mjs), the d5_faces builders (scene builders, not face tools).

**Why:** too many overlapping face tools made every attempt start from a different method. **How to apply:** before writing a new face tool, extend this path instead; a new method goes to experimental/ until the user approves it. Related: [[ps1-faces-always-ps1]], [[ps1-face-poster-then-pixel]], [[heads-tab]], [[foodface-tool]].
