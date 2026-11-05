---
layout: default
title: Dispositions
nav_order: 6
description: "Safe fix, Guided, Report only — the three dispositions every PreFlight finding receives, and the deterministic rule that assigns them."
---

# Dispositions: Safe Fix, Guided, Report Only
{: .no_toc }

## Every finding is a decision, made by a rule
{: .no_toc .text-delta }

---

A scan that only lists problems leaves the hardest question — *what may I safely automate?* — to you, finding by finding. PreFlight answers it up front: **every finding carries exactly one disposition**, assigned by a deterministic rule, identical for every scan of the same project.

| Disposition | Meaning | Who acts |
| :--- | :--- | :--- |
| **Safe fix** | The repair's correctness needs **no guess** in this project. PreFlight can state exactly what will change and prove it is right. | PreFlight — via [preview + one Undo](./repairs) |
| **Guided** | A repair exists, but a human choice is part of it — picking a type, clearing a reference, re-pointing a field. | You, in the Inspector, guided by the finding's evidence and Next Action |
| **Report only** | PreFlight will not repair this in v1. You get the finding, the path, and the evidence — never a repair button it cannot stand behind. | You, manually, if at all |

## The safe rule

> A fix earns the **Safe** label only when its correctness needs **no guess in the project that was scanned**.

Concretely, in v1 the Safe set is:

- A **missing script** whose recorded identity resolves to **exactly one** matching loaded type → relink, preserving the component's surviving field values.
- An **orphaned `.meta`** file whose asset is gone → remove the orphan.
- A **detected scene** absent from EditorBuildSettings → add it to Build Settings.

And the same rule, from the other side:

- A missing script matching **two** types is Guided — you pick from the candidates, shown with full type names.
- A missing script matching **none** is Report only — the recorded identity is in the evidence.
- A **damaged serialized reference** is Guided — clearing or re-pointing it is your call.
- **Broken prefab chains**, **missing `.meta` files** on living assets, and **duplicate GUIDs** are Report only in v1 — the documentation states plainly why, instead of pretending a repair happened.

The rule is environment-sensitive *by design*: the same defect can be Safe in one project and Guided in another, because "safe" is judged against what **this** scan can prove in **this** project. The rule itself never changes — only the proof available to it. The Safe Repair Set is versioned and visible in [Settings](./settings).

## The sample, counted

One scan of the Harborlight Sample (Broken) exercises all three dispositions:

| | Count | Which defects |
| :--- | :---: | :--- |
| Safe fix | **3** | 1 missing-script relink · 1 orphaned `.meta` removal · 1 scene added to Build Settings |
| Guided | **3** | 1 ambiguous missing script · 2 damaged references to clear |
| Report only | **6** | 3 broken prefab chains · 1 unresolvable missing script · 1 missing `.meta` · 1 duplicate GUID |
| **Total** | **12** | 8 errors · 4 warnings |

Because dispositions are assigned by rule, the [verdict file](./verdict-json) can carry them per finding — and your CI can treat "open Safe fixes remain" differently from "a human decision is pending", if you want it to.
