---
layout: default
title: Getting Started
nav_order: 2
description: "The core PreFlight concepts: scans, findings and evidence, dispositions, previewed repairs under one Undo, and the verdict."
---

# Getting Started with PreFlight
{: .no_toc }

## The five ideas behind every PreFlight run
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## 1. One window, four sections

Everything happens in the PreFlight Home window — **Tools → Decnet Games → PreFlight** in the Unity Editor menu. The window has four sections:

- **Scan** — set the scope and scan the project.
- **Repairs** — preview and apply fixes.
- **Reports** — read and export the Markdown report and the verdict.
- **Settings** — the Safe Repair Set and per-class scan switches.

First launch shows a welcome screen with one-click setup. After that there is nothing to configure before your first scan.

![The PreFlight welcome screen on first run]({{ "/assets/images/welcome-first-run.png" | relative_url }})

## 2. A scan produces findings, not vibes

A scan walks your project's Assets and checks five [defect classes](./defect-classes):

| # | Class | In plain language |
| :--- | :--- | :--- |
| 1 | Missing scripts | A component whose script reference no longer resolves to a real type |
| 2 | Broken prefab reference chains | Prefab instances and nested prefabs whose source link or referenced objects are broken |
| 3 | Unassigned references | Serialized object-reference fields holding a broken or missing object |
| 4 | Orphaned `.meta` files and GUID collisions | `.meta` files whose asset is gone; duplicate GUIDs across Assets |
| 5 | Scenes missing from Build Settings | Scene assets in the project that are absent from EditorBuildSettings |

Every **finding** is one concrete defect, listed with its asset path and a plain-language **evidence line** — what was found, where, and why PreFlight believes it is damage rather than an intentionally empty slot.

![Scan results: every finding named, with its evidence]({{ "/assets/images/scan-results.png" | relative_url }})

## 3. Every finding gets a disposition

A finding is never just "an error". Each one is classified as exactly one of:

- **Safe fix** — PreFlight can repair it deterministically, with no guess about your intent.
- **Guided** — a repair exists, but a human choice is part of it (for example, picking which of two matching types was meant).
- **Report only** — PreFlight shows you the damage and the evidence, and does not offer a repair it cannot stand behind.

The full rules are on the [Dispositions](./dispositions) page.

## 4. Repairs are previewed, then applied under one Undo

Nothing is applied silently. The Repairs section shows each proposed fix — finding, action, target — **before** it runs. **Repair All Safe Fixes** applies the whole run as a single Undo transaction, and one Undo restores the pre-repair state. Guided findings stay yours: you resolve them in the Inspector, following the finding's Next Action.

See [Repairs: Preview and One Undo](./repairs).

## 5. Every run ends in a verdict

After every scan and every repair run, PreFlight writes **`preflight-verdict.json`** at your project root: status **PASS** or **FAIL**, finding counts, and a per-finding entry with class, path, disposition and status. The file contains no absolute paths and no user names, so it is safe to commit and share across machines.

The human-readable side is the [Markdown report](./markdown-report): every finding with its Evidence and the one Next Action that clears it.

A PASS verdict means the most recent scan found **zero open findings in the five classes, in the scanned scope**. It is a statement about reference integrity — nothing more, and PreFlight says so itself in [What v1 Is Not](./what-v1-is-not).

---

## Where to go next

- New install? [Installation](./installation), then the [Quick Start](./quick-start).
- Wiring PreFlight into a build pipeline? [Headless & CI](./headless-and-ci).
- Want to watch the whole loop on a known-broken project first? [The Harborlight Sample](./harborlight-sample).
