---
layout: default
title: Settings & the Safe-Fix Rule
nav_order: 13
description: "The Settings section: the versioned Safe Repair Set (v1.0), one switch per defect class, and the deterministic rule that decides what counts as safe."
---

# Settings & the Safe-Fix Rule
{: .no_toc }

## What "safe" means is written down, in the open
{: .no_toc .text-delta }

---

![Settings: the Safe Repair Set (v1.0) and the five scan-class switches]({{ "/assets/images/settings.png" | relative_url }})

## The Safe Repair Set (v1.0)

The Settings section shows the **Safe Repair Set** — the versioned, explicit list of repairs PreFlight is allowed to perform automatically. In v1.0 it contains exactly three repair kinds:

1. **Relink** a missing script whose recorded identity resolves to exactly one matching type — preserving the component's surviving field values.
2. **Remove** an orphaned `.meta` file whose asset is gone.
3. **Add** a detected scene to EditorBuildSettings.

That list *is* the automation boundary. A repair that is not in the Safe Repair Set does not get a Safe disposition, does not appear in Repair All Safe Fixes, and is not run by the headless safe-repair flag. Nothing joins the set silently — it is versioned (v1.0) precisely so a change to it is a visible event.

## The safe-fix rule

> **A fix earns the Safe label only when its correctness needs no guess in the project it was scanned in.**

Two consequences worth understanding:

- **The rule is deterministic.** Scan the same project twice — in the window, headless, on another machine — and every finding gets the same disposition. The automated suite that verifies PreFlight (23/23 tests, on Unity 2022.3 LTS and Unity 6) includes the classification behaviour.
- **The judgement is per-project.** A missing script is Safe in a project where its recorded identity matches exactly one type, and Guided in a project where it matches two. "Safe" is a property of the *proof available in your project*, never a promise about a defect class in the abstract. Which fixes count as safe therefore depends on what a scan can prove in the project in front of it — and anything it cannot prove is handed back to you as Guided or Report only, never forced.

## Scan-class switches

Each of the five [defect classes](./defect-classes) has its own switch in Settings. Turn a class off and scans skip it entirely — its findings do not appear, do not count toward the verdict, and are not written to the [verdict file](./verdict-json).

The default is **all five on**, and that is the configuration every number in this documentation was measured with. Narrowing the scan is legitimate for focused work (a `.meta`-only pass after a merge, for example) — just remember the verdict then certifies only the classes you left on, in the scope you scanned.

## Scope

The scan scope itself is set in the **Scan** section (default: `Assets`). Scope and class switches together define exactly what a verdict covers — PreFlight never claims anything about assets it did not scan. See [What v1 Is Not](./what-v1-is-not) for the full honesty list.
