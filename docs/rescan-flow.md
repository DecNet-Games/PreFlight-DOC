---
layout: default
title: Re-scan Flow
nav_order: 8
description: "The re-scan is the receipt: scan again after repairs and the counts tell the truth — 12 findings to 9 on the sample, 0 on the clean project."
---

# The Re-scan Flow
{: .no_toc }

## Repair is a claim. The re-scan is the proof.
{: .no_toc .text-delta }

---

PreFlight's workflow does not end at "repaired". After every repair run, **scan the same scope again**. The re-scan is the receipt: it shows what the run actually cleared, what remains, and what kind of work the remainder needs.

## The sample, end to end

| Step | Findings | What the count means |
| :--- | :---: | :--- |
| First scan of Harborlight (Broken) | **12** (8 errors, 4 warnings) | 3 Safe fix · 3 Guided · 6 Report only |
| Repair All Safe Fixes | −3 | One transaction, one Undo, logged |
| **Re-scan** | **9** | **0 safe repairs left** — everything remaining is Guided or Report only |
| Scan of Harborlight (Clean) | **0** | **Verdict: PASS** — "No integrity findings in this project." |

![Repaired. Re-scanned. Counted.]({{ "/assets/images/rescanned.png" | relative_url }})

![The post-repair scan in the window: 9 findings remain]({{ "/assets/images/scan-after-repair.png" | relative_url }})

## Reading a re-scan

- **Safe repairs remaining: 0** — the automatic work is done. If a re-scan still shows Safe fixes, the repair run did not apply (or new damage arrived between runs).
- **Guided findings remain** — a human decision is pending: pick the type, clear the reference. Each one names its Next Action in the [Markdown report](./markdown-report).
- **Report-only findings remain** — known damage, documented with evidence, awaiting manual repair (or acceptance). They keep the verdict at FAIL while they are open — that is the verdict doing its job, not crying wolf: FAIL means "open findings exist in the scanned classes", nothing more and nothing less.
- **0 findings** — the verdict flips to **PASS** for that scope.

## The working rhythm

1. **Scan** before you ship, after a merge, after a refactor, after an agent touches files.
2. **Preview → Repair** the safe set.
3. **Re-scan** and work the Guided list with the report open.
4. **Re-scan** until the remaining findings are only the ones you have consciously accepted — then the [verdict file](./verdict-json) is your record of that state, safe to commit next to the build it describes.

> **Pro Tip:** In CI, the same rhythm is one command: scan headlessly, and let the exit code (0 / 1 / 2) decide whether the pipeline proceeds. See [Headless & CI](./headless-and-ci).
