---
layout: default
title: Missing Scripts
parent: Defect Classes
nav_order: 1
description: "Class 1 — components whose script reference no longer resolves to a real type, and how PreFlight relinks, guides, or reports them."
---

# Class 1 — Missing Scripts
{: .no_toc }

---

## The defect

A component on a GameObject or prefab whose script reference no longer resolves to a real type. In the Inspector it shows as a missing-script warning; in the project it is a behaviour that silently no longer exists. The usual causes: a script file renamed or deleted, a class renamed in code, an assembly that moved.

![A missing script on a real prefab, before repair]({{ "/assets/images/inspector-before.png" | relative_url }})

## What PreFlight reports

For each missing script, PreFlight records the component's **recorded type identity** — the class name and namespace captured in the asset's serialization — and checks it against the types actually loaded in your project. The finding's evidence line names the asset, the target object, and how the recorded identity resolved.

## The three outcomes — all three occur on the sample

The Harborlight sample plants one missing script of each kind, which is the fastest way to see the rule:

| Sample defect | Recorded identity resolves to… | Disposition |
| :--- | :--- | :--- |
| `NPC_Patrol` prefab component (`Harborlight.EnemyPatrol`) | exactly **one** loaded type | **Safe fix** — relink |
| `PierLamp` scene component | **two** loaded types in different namespaces | **Guided** — you pick |
| `DockCrane` prefab component | **no** loaded type | **Report only** |

- **Safe — relink.** When the recorded identity matches exactly one type, PreFlight relinks the component to that type. The component's surviving serialized field values are preserved: on the sample, the relinked `NPC_Patrol` comes back as a working Enemy Patrol component with its Patrol Speed 3.5, Patrol Radius 10 and Waypoint Count 4 untouched.
- **Guided — type selector.** When the name matches two types, guessing would be a coin flip. PreFlight shows the candidates with full type names and you choose.
- **Report only.** When the type exists nowhere in the loaded assemblies, there is nothing legitimate to relink to. The finding carries the recorded identity as evidence so you can hunt the original script down yourself.

> **The rule, stated once:** a missing script is a Safe fix only when its recorded identity resolves to **exactly one** matching type in the project that was scanned. That is the [safe-fix rule](./../settings) applied to this class — deterministic, and identical on every machine that scans the same project.

Repairs from this class run through the standard [preview + one Undo](./../repairs) flow, like every PreFlight repair.
