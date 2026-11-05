---
layout: default
title: Harborlight Sample
nav_order: 12
description: "The included Harborlight Sample (Broken): a pier scene with 12 deliberate defects — the full defect catalogue, and the walkthrough that repairs it."
---

# The Harborlight Sample (Broken)
{: .no_toc }

## Practise on the sample. Ship your own.
{: .no_toc .text-delta }

---

The package ships a self-contained demonstration project: **Harborlight**, a small pier scene whose assets carry **12 deliberate reference defects** — every flaw in it is planted, catalogued, and safe to experiment on. Its twin, **Harborlight (Clean)**, is the same project with none of the damage.

![The Harborlight sample scene, exactly as it ships]({{ "/assets/images/harborlight-scene.png" | relative_url }})

Use the sample to learn the loop — and to verify your install — before scanning anything you care about: a healthy PreFlight install reproduces this page's numbers exactly.

## Walkthrough

1. Open the PreFlight Home window (**Tools → Decnet Games → PreFlight**) and run **Setup** once — it answers "PreFlight is ready."
2. In the **Scan** section, set the scan scope to the **Harborlight Sample (Broken)** and run the scan. Verdict: **FAIL — 12 findings (8 errors, 4 warnings)**.
3. In **Repairs**, read the preview, then **Repair All Safe Fixes**: the 3 safe repairs apply under one Undo.
4. **Re-scan** the same scope: **9 findings**, 0 safe repairs remaining.
5. Resolve the 3 Guided findings in the Inspector if you want the full exercise (the [report](./markdown-report) names each Next Action); the 6 Report-only findings stay documented, by design.
6. Scan **Harborlight (Clean)**: **0 findings — Verdict: PASS.**

The same walkthrough with timings is the [Quick Start](./quick-start); the end-to-end flow on the sample measured **57.6 seconds**.

## The defect catalogue

The 12 planted defects, exactly as the sample's own defect manifest records them:

| ID | Class | Planted defect | Target | Disposition |
| :--- | :--- | :--- | :--- | :--- |
| PF-D01 | Missing script | Component whose recorded type (`Harborlight.EnemyPatrol`) exists as exactly one loaded type | `NPC_Patrol` prefab | **Safe** — relink |
| PF-D02 | Missing script | Component whose recorded class name matches two loaded types in different namespaces | `PierLamp` (scene) | **Guided** — you pick the type |
| PF-D03 | Missing script | Component whose recorded type exists nowhere in the loaded assemblies | `DockCrane` prefab | Report only |
| PF-D04 | Broken prefab chain | Nested prefab instance whose source prefab asset is deleted | `PierSection_MissingSource` in `DockComplex` | Report only (v1) |
| PF-D05 | Broken prefab chain | Prefab variant whose base-prefab link is broken | `PierCrate_Variant` | Report only (v1) |
| PF-D06 | Unassigned reference | Scene object field holding a destroyed object's instance ID | `HarborMaster` (scene) | **Guided** — reference clearing |
| PF-D07 | Unassigned reference | ScriptableObject field holding an unresolvable object reference | `HarborSettings` asset | **Guided** — reference clearing |
| PF-D08 | Meta / GUID | `.meta` file whose asset was deleted | `pier_weathered_wood.png.meta` | **Safe** — remove orphan |
| PF-D09 | Meta / GUID | Asset whose `.meta` file is absent | `cargo_manifest.txt` | Report only |
| PF-D10 | Meta / GUID | Two assets sharing one GUID in their `.meta` files | `PierWood.mat` / `PierRope.mat` | Report only |
| PF-D11 | Build Settings | The sample's second scene is absent from EditorBuildSettings | `HarborlightWarehouse.unity` | **Safe** — add scene |
| PF-D12 | Broken prefab chain | Instance override targeting a component that no longer exists on the source | `PierCrate_Instance` (scene) | Report only (v1) |

Totals: **3 Safe · 3 Guided · 6 Report only** — one scan exercises every disposition and nearly every repair path PreFlight has. The per-class pages ([Missing Scripts](./defect-classes/missing-scripts), [Broken Prefab Chains](./defect-classes/broken-prefab-chains), [Unassigned References](./defect-classes/unassigned-references), [Meta Files & GUIDs](./defect-classes/meta-files-and-guids), [Scenes & Build Settings](./defect-classes/scenes-and-build-settings)) use these same defects as their worked examples.

> **Resetting the sample:** repaired the sample and want it broken again? One Undo reverses a repair run; for a full reset, re-import the sample from the package (Package Manager → PreFlight → Samples) or restore the sample folder from your version control.
