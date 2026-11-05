---
layout: default
title: Support
nav_order: 16
description: "PreFlight support: email Decnet Games, join the Discord community, and what to include when you report a problem."
---

# Support
{: .no_toc }

---

## Email

**support@decnetgames.com** — PreFlight is made and supported directly by Decnet Games.

## Community

Join the Decnet Games Discord: **https://discord.gg/P9wepz7NBW** — questions, findings from the field, and discussion with other PreFlight users.

More Decnet Games tools live on the publisher page: **https://assetstore.unity.com/publishers/118262**.

## Reporting a problem — what to include

A good report gets a fast, useful answer. Please include:

1. **Your Unity version** (for example 2022.3 LTS or the exact Unity 6 build) and your Editor platform.
2. **What you ran** — a window scan or the headless command (paste the command line), and the scope you scanned.
3. **The verdict file.** Attach the run's `preflight-verdict.json`. It is safe to share by design: it contains no absolute paths and no user names — only the project hash, counts, and per-finding class/path/disposition/status.
4. **The finding in question.** If one finding looks wrong, quote its **Evidence** line from the [Markdown report](./markdown-report) and say what you expected instead. Classification disagreements are exactly the reports that improve the [safe-fix rule](./settings).

## Before you write

- The [FAQ](./faq) answers the recurring questions — what PASS certifies, why a finding is Guided rather than Safe, and how the CI exit codes work.
- [What v1 Is Not](./what-v1-is-not) lists the deliberate v1 boundaries. If your request is outside them, it is still worth sending — boundaries move between versions, and user reports are how that happens — but it helps to know it is a boundary rather than a bug.
