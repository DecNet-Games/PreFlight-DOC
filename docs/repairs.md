---
layout: default
title: Repairs — Preview & One Undo
nav_order: 7
description: "How PreFlight repairs work: a full preview before anything is applied, Repair All Safe Fixes as a single Undo transaction, and a repair log of everything the run did."
---

# Repairs: Preview First, One Undo
{: .no_toc }

## Nothing is applied silently
{: .no_toc .text-delta }

---

## 1. The preview

Open the **Repairs** section after a scan. For every finding with the **Safe fix** [disposition](./dispositions), the preview lists three things before anything runs:

- **Finding** — the defect, with its evidence line.
- **Action** — exactly what the repair will do.
- **Target** — the asset and object it will touch.

![Repairs preview — every repair visible before it touches the project]({{ "/assets/images/repairs-preview.png" | relative_url }})

If a preview line surprises you, stop there: **nothing has been applied yet.** Guided findings appear in the same section for reference, but they are yours to resolve in the Inspector — PreFlight does not apply them. Report-only findings carry no repair action at all.

## 2. Repair All Safe Fixes

Click **Repair All Safe Fixes** and the run applies every previewed safe fix as **one Undo transaction** — not one transaction per fix. The window reports the run in its own words; on the sample:

> "Successfully repaired 3 issues under single Undo transaction."

The **repair log** lists everything the run did, finding by finding, and the post-repair state is written to [`preflight-verdict.json`](./verdict-json) like every other run.

![After the repair run: the missing script is a working component again, values intact]({{ "/assets/images/repairs-after.png" | relative_url }})

## 3. One Undo restores everything

Because the whole run is a single transaction, **one Undo** restores the complete pre-repair state — relinked scripts, the removed `.meta`, the Build Settings list, all of it. The window confirms:

> "Undid last repair transaction."

![One Undo: the full repair transaction rolled back]({{ "/assets/images/repairs-undo.png" | relative_url }})

This is the working rhythm PreFlight is built for: scan, preview, repair, [re-scan](./rescan-flow) — and if the re-scan or your own inspection shows anything unexpected, one Undo puts the project back exactly where it was before the run.

## 4. What repairs never do

- **Never guess.** A fix that needs a judgement call is Guided or Report only — see the [safe-fix rule](./settings).
- **Never substitute.** If a piece of a repair cannot be performed as previewed, it is not silently replaced with a different one.
- **Never reach outside the run.** Repairs touch only the previewed targets, and the run writes only inside your project and to the verdict and report paths shown in the window.
- **Never run by default in headless mode.** The CI entry point scans and reports only, unless you explicitly pass the safe-repair flag — see [Headless & CI](./headless-and-ci).
