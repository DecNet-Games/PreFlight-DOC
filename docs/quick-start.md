---
layout: default
title: Quick Start
nav_order: 4
description: "The full PreFlight loop on the included Harborlight sample — scan, preview, repair under one Undo, re-scan — then the same loop on your own project."
---

# Quick Start
{: .no_toc }

## Five minutes, one broken sample, one verdict
{: .no_toc .text-delta }

1. TOC
{:toc}

---

This walkthrough runs the complete PreFlight loop on the **Harborlight Sample (Broken)** that ships in the package — a small pier scene with deliberate defects — before you point PreFlight at your own assets. Every number below is what the sample actually produces.

## 1. Open the PreFlight window

In the Unity Editor menu, select **Tools → Decnet Games → PreFlight**. On first launch, the welcome screen appears.

## 2. Run Setup

Click **Run Setup / Verify Install**. PreFlight verifies the install and answers **"PreFlight is ready."** (Run it again and it answers "Already set up — nothing changed." — setup is idempotent.)

## 3. Scan the sample

Go to the **Scan** section and set the scan scope to the **Harborlight Sample (Broken)**, then run the scan.

PreFlight inspects the sample's assets across the [five defect classes](./defect-classes). The verdict banner shows **FAIL**, and the findings appear grouped by class, each with a plain-language evidence line:

- **12 findings — 8 errors and 4 warnings**
- **3 Safe fix · 3 Guided · 6 Report only**

![The sample scan: 12 findings, grouped by class]({{ "/assets/images/scan-results.png" | relative_url }})

The full defect-by-defect breakdown of this exact scan is catalogued on the [Harborlight Sample](./harborlight-sample) page.

## 4. Preview the repairs

Open the **Repairs** section. Before anything is applied, the preview lists each proposed safe fix — finding, action, target. The sample has **3 safe repairs** waiting: a missing script that relinks to its one matching type, an orphaned `.meta` file to remove, and a detected scene to add to Build Settings. The 3 Guided findings are left to you in the Inspector; the 6 Report-only findings carry their evidence and no repair button.

![Repairs preview: see every repair before it touches your project]({{ "/assets/images/repairs-preview.png" | relative_url }})

## 5. Repair All Safe Fixes — one transaction, one Undo

Click **Repair All Safe Fixes**. PreFlight applies the three repairs as a single Undo transaction and reports in its own words: **"Successfully repaired 3 issues under single Undo transaction."**

Changed your mind? One **Undo** restores the pre-repair state completely — the window confirms with **"Undid last repair transaction."** The repair log lists everything the run did, either way.

## 6. Re-scan and read the verdict

Run the scan again on the same scope. The count is now **12 findings → 9**: the safe repairs are gone, zero safe repairs remain, and what is left is guided or report-only — PreFlight does not guess at those to make the number prettier.

![Re-scanned after repair: 12 findings before, 9 after]({{ "/assets/images/scan-after-repair.png" | relative_url }})

Now scan the sample's clean twin, **Harborlight (Clean)**: the run ends at **0 findings** with the verdict banner on **PASS** — "No integrity findings in this project."

![The clean twin: Verdict PASS, zero findings]({{ "/assets/images/verdict-clean.png" | relative_url }})

After every scan and repair run, PreFlight has also written **`preflight-verdict.json`** at the project root — the machine-readable form of the same verdict, ready for CI and tooling. See [Verdict JSON](./verdict-json).

In verification, this whole open-to-verdict flow on the sample timed **57.6 seconds**, end to end.

## 7. Now scan your own project

Set the scan scope back to `Assets` in the Scan section and click **Scan This Project**.

> **Pro Tip:** Run PreFlight whenever an agent, a merge, or a refactor touches your project files — and once more right before you ship. If you would rather gate automatically than remember, the same scan runs headless with a 0 / 1 / 2 exit-code contract: see [Headless & CI](./headless-and-ci).
