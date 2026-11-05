---
layout: default
title: Defect Classes
nav_order: 5
has_children: true
description: "The five integrity defect classes one PreFlight scan checks: missing scripts, broken prefab chains, unassigned references, meta/GUID damage, and scenes missing from Build Settings."
---

# Defect Classes
{: .no_toc }

## What one scan actually looks for
{: .no_toc .text-delta }

---

One PreFlight scan checks your project's Assets against **five defect classes** — the five ways Unity project references rot in real work: renames, merges, deletions and hand-edited files. Each class has its own page with what the defect is, what PreFlight reports, and which repairs exist for it.

| # | Class | Findings on the Harborlight sample | Safe | Guided | Report only |
| :--- | :--- | :---: | :---: | :---: | :---: |
| 1 | [Missing Scripts](./defect-classes/missing-scripts) | 3 | 1 | 1 | 1 |
| 2 | [Broken Prefab Chains](./defect-classes/broken-prefab-chains) | 3 | 0 | 0 | 3 |
| 3 | [Unassigned References](./defect-classes/unassigned-references) | 2 | 0 | 2 | 0 |
| 4 | [Meta Files & GUIDs](./defect-classes/meta-files-and-guids) | 3 | 1 | 0 | 2 |
| 5 | [Scenes & Build Settings](./defect-classes/scenes-and-build-settings) | 1 | 1 | 0 | 0 |
| | **Total** | **12 (8 errors, 4 warnings)** | **3** | **3** | **6** |

![Five defect classes — every one named, every finding given a disposition]({{ "/assets/images/five-classes.png" | relative_url }})

The sample column is measured, not illustrative: it is the scan of the [Harborlight Sample (Broken)](./harborlight-sample) exactly as it ships, defect for defect. Your project will produce different counts — the classes, the evidence lines and the [disposition rules](./dispositions) are the same.

Each class can be switched off independently in [Settings](./settings) if you ever need a narrower scan — the default is all five on.
