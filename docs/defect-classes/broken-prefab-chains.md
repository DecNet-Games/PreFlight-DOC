---
layout: default
title: Broken Prefab Chains
parent: Defect Classes
nav_order: 2
description: "Class 2 — prefab instances, nested prefabs and variants whose source link or referenced objects are broken. Detected and reported in v1; never silently rebuilt."
---

# Class 2 — Broken Prefab Reference Chains
{: .no_toc }

---

## The defect

Prefab structure that no longer connects: an instance whose source prefab is gone, a nested prefab whose source asset was deleted, a variant whose base-prefab link is broken, or an instance override that targets a component which no longer exists on the source. These break quietly — the scene still opens, the object still renders, and the link is simply dead.

## What v1 does with this class — honestly

**Detection and reporting. Not reconstruction.**

PreFlight does **not** reconstruct broken prefab hierarchies or rewrite nested component graphs. Rebuilding a chain would mean inventing structure you never authored — exactly the kind of guess PreFlight exists to avoid. Instead, every broken link is reported with its asset path and a plain-language evidence line, so you can repair the chain yourself with full knowledge of what broke.

This is a deliberate v1 boundary, stated in the package's own *What v1 Is Not* page and repeated in [What v1 Is Not](./../what-v1-is-not) here.

## The sample plants three

All three broken-chain defects in the Harborlight sample are Report only in v1:

| Sample defect | What broke | Disposition |
| :--- | :--- | :--- |
| `PierSection_MissingSource` in `DockComplex.prefab` | Nested prefab instance whose source prefab asset was deleted | Report only |
| `PierCrate_Variant` | A prefab variant whose base-prefab link is broken | Report only |
| `PierCrate_Instance` in the sample scene | An instance override targeting a component that no longer exists on the source | Report only |

## Reading a broken-chain finding

Each finding names the asset that holds the broken link and the target that failed to resolve. The [Markdown report](./../markdown-report) gives the same finding a **Next Action** — the manual step that clears it (typically: re-link the instance to the correct source prefab, re-base the variant, or remove the dead override in the Inspector).

Finding these early is the value: a broken chain discovered by a scan is a five-minute fix; the same chain discovered by a buyer, or by a failed build, is not.
