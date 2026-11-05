---
layout: default
title: Unassigned References
parent: Defect Classes
nav_order: 3
description: "Class 3 — serialized object-reference fields holding a broken or missing object, where the field's state shows damage rather than an intentionally empty slot."
---

# Class 3 — Unassigned References
{: .no_toc }

---

## The defect

A serialized object-reference field — on a scene object, a prefab, or a ScriptableObject — that points at an object which no longer exists: the referenced object was destroyed, or its instance ID no longer resolves to anything in the project. At run time this is the reference that throws, or the behaviour that silently does nothing.

## Damage vs. an intentionally empty slot

Not every empty field is a defect. A reference field that was **never assigned** is a normal state in plenty of designs — a slot you fill per-instance, an optional hook. PreFlight distinguishes the two by the field's state: it reports a finding where the serialized state shows **damage** — a reference that was written and whose target is now unresolvable — rather than an intentionally empty slot. The finding's evidence line states which case was found and where.

## Disposition in v1: Guided

Clearing a damaged reference is a real repair, but it changes your data — so in v1 it is **Guided**, not automatic:

- PreFlight locates the field precisely (asset, object, field) and shows the evidence.
- **You** clear or re-point the reference in the Inspector, following the finding's Next Action in the [Markdown report](./../markdown-report).
- A re-scan confirms the finding is gone.

PreFlight will not clear fields behind your back: a reference you *meant* to re-point to a different object looks identical to one you meant to clear, and choosing between those is your call, not a scanner's.

## The sample plants two

| Sample defect | Where | Disposition |
| :--- | :--- | :--- |
| `HarborMaster` | A scene object's reference field holding a destroyed object's instance ID | Guided — reference clearing |
| `HarborSettings` | A ScriptableObject asset field holding an unresolvable object reference | Guided — reference clearing |

Both survive the sample's Repair All Safe Fixes run — they are two of the nine findings still standing in the [re-scan](./../rescan-flow), waiting on a human decision, exactly as designed.
