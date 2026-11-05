---
layout: default
title: Scenes & Build Settings
parent: Defect Classes
nav_order: 5
description: "Class 5 — scene assets that exist in the project but are absent from EditorBuildSettings, and the one-click safe repair that adds them."
---

# Class 5 — Scenes Missing from Build Settings
{: .no_toc }

---

## The defect

A scene asset that exists in the project but is absent from **EditorBuildSettings** — so it is silently excluded from every build. The scene works in the Editor, playtests fine, and simply is not there when the game ships or when other scenes try to load it by build index.

The usual story is mundane: the scene was created, saved, and never added to the build list — or the build list was overwritten by a merge.

## What PreFlight reports

Every `.unity` scene asset in the scanned scope that does not appear in EditorBuildSettings, with its full asset path in the evidence line.

## Disposition: Safe fix

Adding a detected scene to Build Settings is deterministic — the scene exists, the list exists, the repair is a pure addition with no interpretation involved:

- **Safe fix** — Repair All Safe Fixes appends the scene to EditorBuildSettings as part of the run's single Undo transaction. If you undo the run, the build list returns to its previous state with everything else.

The sample plants exactly one: its second scene, `Scenes/HarborlightWarehouse.unity`, missing from the build list — repaired by the sample's safe-fix run and counted in the 12 → 9 [re-scan](./../rescan-flow).

> **Scope note:** like every class, this check runs over the scope you scanned. A scene outside the scanned scope is neither reported nor added — set the scope to `Assets` for a whole-project check, as the [Quick Start](./../quick-start) does for your own project.
