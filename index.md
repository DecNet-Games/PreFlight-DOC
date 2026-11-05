---
layout: default
title: Home
nav_order: 1
description: "PreFlight finds what is broken in your Unity project before you ship: one scan across five defect classes, previewed repairs under one Undo, and a verdict file your tools can read."
permalink: /
---

# PreFlight — Project Integrity Scanner
{: .fs-9 }

Find what is broken in your project. Repair what can be repaired. Get a verdict your tools can read.
{: .fs-6 .fw-300 }

[Getting Started](./docs/getting-started){: .btn .btn-primary .fs-5 .mb-4 .mb-md-0 .mr-2 } [Installation](./docs/installation){: .btn .fs-5 .mb-4 .mb-md-0 }

![PreFlight — find what is broken in your project]({{ "/assets/images/cover.png" | relative_url }})

---

## Your project can look fine and still ship broken

A Unity project can look completely healthy and still be carrying damage: a script that was renamed and left a component missing, a prefab whose reference chain broke in a merge, a serialized field pointing at an object that no longer exists, a `.meta` file orphaned from its asset, a scene that never made it into Build Settings. You usually find out at the worst possible moment — in review, in a failed build, or in a buyer's project.

**PreFlight is the check you run before that moment.** One scan of your project's Assets across five integrity defect classes, a repair pass that only touches what it can prove, and a verdict at the end of every run.

![One scan, previewed repairs, and the verdict — the full PreFlight loop]({{ "/assets/images/scan-repair-verdict.gif" | relative_url }})

<video controls preload="metadata" style="max-width: 100%">
  <source src="{{ "/assets/videos/demo.mp4" | relative_url }}" type="video/mp4">
  Your browser does not support the video tag. The same loop — scan, preview, repair, verdict — is documented step by step in the Quick Start.
</video>

---

## The loop: Scan → Preview → Repair → Verdict

1. **Scan** — one pass over your Assets finds defects in [five classes](./docs/defect-classes): missing scripts, broken prefab reference chains, unassigned serialized references, orphaned `.meta` files and GUID collisions, and scenes missing from Build Settings. Every finding carries a plain-language evidence line.
2. **Preview** — every finding gets a [disposition](./docs/dispositions): **Safe fix**, **Guided**, or **Report only**. PreFlight never shows a repair button for a finding it cannot actually repair.
3. **Repair** — safe fixes are previewed as finding, action and target before anything is applied, then run as **one Undo transaction**. One Undo restores the pre-repair state.
4. **Verdict** — every run ends with PASS or FAIL, written to [`preflight-verdict.json`](./docs/verdict-json) at your project root and to a [Markdown report](./docs/markdown-report) with the one Next Action that clears each finding.

---

## Proven on the included sample

The Harborlight Sample (Broken) ships in the package — a small pier scene carrying deliberate defects, scanned exactly as it ships:

| Measured on the sample | Result |
| :--- | :--- |
| One scan | **12 findings — 8 errors, 4 warnings** |
| Dispositions | 3 Safe fix · 3 Guided · 6 Report only |
| After safe repairs, re-scanned | 12 findings → **9** |
| The sample's clean twin | **0 findings — Verdict: PASS** |
| Full open-to-verdict flow | **57.6 seconds**, end to end |

Walk it yourself in the [Harborlight Sample](./docs/harborlight-sample) page, or take the same loop headless in CI with the [Headless & CI guide](./docs/headless-and-ci).

---

## Built for gates, not just for eyeballs

- **Headless by design** — a documented batchmode entry point exits **0 on PASS, 1 on FAIL, 2 on a PreFlight error**, so a CI job, a pre-commit hook, or an AI agent can gate on the same verdict you see in the window.
- **Repairs that never guess** — a fix earns the Safe label only when its correctness needs no guess in the project that was scanned. Anything PreFlight cannot prove is handed back as Guided or Report only, never forced. See the [safe-fix rule](./docs/settings).
- **Local and quiet** — editor-only tooling for Windows, macOS and Linux editors. No third-party dependencies, no network calls, no telemetry, no analytics. It writes only inside your project and to the verdict and report paths shown in the window.
- **Compatible** — Unity **2022.3 LTS** and **Unity 6**, verified on both; the automated suite passes **23/23** across repeated runs.

> **Pro Tip:** Run PreFlight whenever an agent, a merge, or a refactor touches your project files — and always once more right before you package a build for the Asset Store. A PASS means zero open findings in the five scanned classes, in the scope you scanned. What a PASS does *not* mean is listed honestly in [What v1 Is Not](./docs/what-v1-is-not).

---

## Start here

- [Getting Started](./docs/getting-started) — the core concepts in five minutes
- [Installation](./docs/installation) — Asset Store install and one-click setup
- [Quick Start](./docs/quick-start) — the full loop on the sample, then on your own project
- [Defect Classes](./docs/defect-classes) — exactly what one scan finds, class by class
- [Support](./docs/support) — email and community
