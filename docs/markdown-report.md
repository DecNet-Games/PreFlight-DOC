---
layout: default
title: Markdown Report
nav_order: 10
description: "The human-readable side of every run: a Markdown report where every finding carries its Evidence and the one Next Action that clears it."
---

# The Markdown Report
{: .no_toc }

## A report that tells you what to do next
{: .no_toc .text-delta }

---

The [verdict JSON](./verdict-json) is for machines. The **Markdown report** is the same run, written for the human who has to fix things.

Export it from the **Reports** section with **Export Report (Markdown)** — or read it in the window — after any scan or repair run.

![The Markdown report: findings grouped by class, each with Evidence and Next Action]({{ "/assets/images/report.png" | relative_url }})

## What every finding entry contains

Findings are grouped by [defect class](./defect-classes), and every single entry carries:

- **The finding** — what is broken, and the asset path it lives at.
- **Evidence** — the plain-language line that justifies the finding: the recorded type identity and how it resolved, the target that no longer exists, the GUID two assets share. Evidence is what separates a finding from a guess — and it is what you check when a finding surprises you.
- **Disposition** — [Safe fix, Guided, or Report only](./dispositions).
- **Next Action** — the one step that clears this finding. For a Safe fix, that is "run the repair"; for a Guided finding, the exact manual move (pick this type, clear this field in the Inspector); for Report only, the manual repair the evidence points at.

## How the report gets used

- **Solo:** work the Guided list top to bottom, report open, Inspector beside it. [Re-scan](./rescan-flow) after each pass.
- **In review:** attach the report to the pull request or the release checklist — it is the standing record of what was broken, what was repaired under Undo, and what was consciously left open.
- **With agents:** an AI agent (or a teammate) can work from the report alone: every entry is self-contained — path, evidence, next action — with no window state required.

The report and the verdict file are two renderings of one run: same findings, same counts, same dispositions. When they would disagree, that is a bug — tell us via [Support](./support) and include the verdict file (it contains no absolute paths or user names, by design).
