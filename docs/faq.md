---
layout: default
title: FAQ
nav_order: 15
description: "PreFlight questions answered: compatibility, what PASS means, whether repairs can be undone, CI behaviour, privacy, and the sample."
---

# Frequently Asked Questions
{: .no_toc }

---

## Which Unity versions and platforms are supported?

Unity **2022.3 LTS** and **Unity 6**, verified on both (the automated suite passes 23/23 across repeated runs). PreFlight is editor-only tooling for **Windows, macOS and Linux editors** and adds nothing to your player build. There are **no third-party dependencies**.

## What does a PASS verdict actually certify?

That the most recent scan found **zero open findings in the five defect classes, in the scope you scanned** — reference integrity, in that scope. It does not certify that your gameplay logic, third-party libraries or shaders are correct, and PreFlight never claims your project "works" or "builds". The full honesty list is [What v1 Is Not](./what-v1-is-not).

## Can a repair break my project?

Repairs are built to be reversible and conservative:

- You see a **preview** — finding, action, target — before anything is applied.
- A fix is only offered automatically when it needs **no guess** in your project (the [safe-fix rule](./settings)).
- **Repair All Safe Fixes** runs as **one Undo transaction**: one Undo restores the complete pre-repair state, and a repair log lists everything the run did.

If a "repair" would require judgement — which type was meant, whether a reference should be cleared or re-pointed — PreFlight marks it Guided and leaves it to you.

## Why is a finding I expected not marked as a Safe fix?

Because "safe" is judged against what the scan can prove **in your project**. The classic case: a missing script whose recorded name matches two different types is Guided, even though the same defect is a Safe relink in a project where it matches exactly one. See [Dispositions](./dispositions) for the rule and the per-class outcomes.

## Does PreFlight fix broken prefab chains?

It **detects and reports** them — asset, target, evidence, and a Next Action in the report — but v1 does not reconstruct prefab hierarchies or rewrite nested component graphs. Rebuilding a chain would mean inventing structure you never authored. See [Broken Prefab Chains](./defect-classes/broken-prefab-chains).

## Can I run PreFlight in CI?

Yes — that is a primary use. The batchmode entry point runs the same scan headlessly and exits **0 on PASS, 1 on FAIL, 2 on a PreFlight error**. Safe repairs are **off by default** headless; pass `-preflightSafeRepair` to enable them. Full command and argument reference: [Headless & CI](./headless-and-ci).

## Does PreFlight phone home or collect analytics?

No. PreFlight runs entirely on your machine: **no network calls, no telemetry, no analytics**. It writes only inside your project and to the verdict and report paths shown in the window. The verdict file itself contains no absolute paths and no user names, specifically so it is safe to commit and share.

## Where do the verdict and report live?

`preflight-verdict.json` is written at your **project root** after every scan and repair run (headless runs can redirect it with `-preflightVerdictPath`). The Markdown report is exported from the **Reports** section. Formats: [Verdict JSON](./verdict-json) · [Markdown Report](./markdown-report).

## What is the Harborlight sample for?

It is a small pier scene with **12 deliberate defects** covering every class and every disposition — a safe place to learn the loop and to verify your install (a correct install reproduces its numbers exactly: 12 findings, 3 safe repairs, 12 → 9 on re-scan, 0 on the clean twin). Walkthrough and full defect catalogue: [Harborlight Sample](./harborlight-sample).

## PreFlight flagged a reference field I intentionally leave empty. Why?

It shouldn't have: PreFlight distinguishes a **damaged** reference (a target was written and no longer resolves) from an **intentionally empty** slot, and reports the damaged case. If you have a field whose state shows damage but is intentional in your design, resolve it as Guided once (assign or clear it deliberately) and the re-scan will be clean — and if you believe the classification itself is wrong, send the finding's evidence line to [Support](./support).

## Does PreFlight work with version control?

It is VCS-agnostic: it works on the files in your project, whatever system tracks them. It is deliberately **not** a VCS client — no commits, checkouts, or merge resolution. Its job after a bad merge is detection: the `.meta` damage and GUID collisions a merge leaves behind are exactly what Class 4 finds.
