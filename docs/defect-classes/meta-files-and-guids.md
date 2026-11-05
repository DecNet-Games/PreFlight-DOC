---
layout: default
title: Meta Files & GUIDs
parent: Defect Classes
nav_order: 4
description: "Class 4 — orphaned .meta files whose asset is gone, assets whose .meta is missing, and duplicate GUIDs shared by two assets."
---

# Class 4 — Orphaned `.meta` Files and GUID Collisions
{: .no_toc }

---

## Why `.meta` damage matters

Every asset in a Unity project carries a `.meta` file holding its GUID — the identity every other asset uses to reference it. When the file pair and the GUID graph rot, references rot with them, and the damage usually surfaces far away from its cause: a texture that silently unlinks, two assets fighting over one identity after a bad merge or a hand-copied folder.

PreFlight checks three forms of this damage:

## The three checks

### Orphaned `.meta` — Safe fix

A `.meta` file whose asset was deleted. The leftover is dead weight with a live GUID, and the fix needs no guess: the asset is gone, so the orphan is removed.

- The sample plants one: `Textures/pier_weathered_wood.png.meta`, left behind by its deleted texture. **Disposition: Safe fix** — removed by Repair All Safe Fixes.

### Missing `.meta` — Report only

An asset whose `.meta` file is absent. Unity will regenerate a `.meta` on next import — with a **new** GUID, which silently severs every existing reference to that asset. PreFlight reports it so you can restore the original `.meta` from version control instead of accepting a new identity by accident.

- The sample plants one: `Documentation/cargo_manifest.txt`. **Disposition: Report only** in v1 — stated plainly, instead of pretending a repair happened.

### Duplicate GUIDs — Report only

Two assets whose `.meta` files carry the **same** GUID — the classic result of copying an asset folder by hand or a merge resolved the wrong way. One of the two identities has to change, and which one keeps the GUID determines which references survive. That judgement is yours.

- The sample plants one pair: `Materials/PierWood.mat` and `Materials/PierRope.mat` sharing one GUID. **Disposition: Report only**, with both paths in the evidence line.

## What PreFlight is not, here

PreFlight **detects and reports** `.meta` damage and GUID collisions; it is **not a version-control client**. It performs no commits, checkouts, or merge-conflict resolutions — restoring files from your VCS history stays your workflow. The scan's job is to make sure you *know*, with paths and evidence, before the damage propagates.
