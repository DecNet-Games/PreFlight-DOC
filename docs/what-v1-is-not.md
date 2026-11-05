---
layout: default
title: What v1 Is Not
nav_order: 14
description: "PreFlight's explicit limits: not a runtime tool, not a universal repairer, not a VCS client, not a cloud service, not a project-health certification."
---

# What PreFlight v1 Is Not
{: .no_toc }

## The boundaries, stated by the product itself
{: .no_toc .text-delta }

---

To maintain absolute reliability and clear operational boundaries, PreFlight defines clear limits on its v1 scope. This page ships inside the package as well — it is reproduced here because a tool you gate builds on should tell you what it will *not* do before you have to find out.

- **Not a Runtime or Player Tool.** PreFlight executes exclusively inside the Unity Editor and headless batchmode. No PreFlight code runs in standalone builds or players.
- **Not a Universal Asset Repairer.** PreFlight does not reconstruct broken prefab hierarchies, rewrite nested component graphs, or restore asset binaries. It repairs what can be deterministically relinked without guessing buyer intent. ([Broken prefab chains](./defect-classes/broken-prefab-chains) are detected and reported, not rebuilt.)
- **Not an Automated Git or VCS Client.** PreFlight detects damaged `.meta` files, duplicate GUID collisions, and missing scene references. It does not perform git commits, checkouts, or merge conflict resolutions.
- **Not a Cloud or Network Service.** PreFlight runs 100% locally on your workstation or CI server. It transmits no telemetry and requires no external network connection.
- **Not an Autonomous AI Agent.** PreFlight provides a deterministic file contract (headless CLI + structured JSON verdict) that agents can read and execute. PreFlight itself does not invoke LLMs or external agents.
- **Not a Universal Project Health Certification.** A `PASS` verdict confirms that no integrity defects within PreFlight's five scanned classes are present — in the scope that was scanned. It does not certify that gameplay logic, third-party libraries, or shader assets are bug-free.

## And in one paragraph, from the listing

A PASS verdict means the most recent scan found zero open findings in the five classes, in the scanned scope. Which fixes count as safe depends on what a scan can prove in the project in front of it — the rule is deterministic and documented, and anything it cannot prove is handed back to you as guided or report-only, never forced. PreFlight certifies **reference integrity** — nothing more, and it would rather tell you that on this page than let a green banner imply otherwise.
