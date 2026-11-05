---
layout: default
title: Headless & CI
nav_order: 11
description: "Run PreFlight in batchmode: the executeMethod entry point, command-line arguments, and the 0 / 1 / 2 exit-code contract for CI gates, pre-commit hooks and agent loops."
---

# Headless & CI Integration
{: .no_toc }

## The same scan, with nobody watching
{: .no_toc .text-delta }

1. TOC
{:toc}

---

PreFlight exposes a batchmode entry point designed for automated build pipelines, pre-commit hooks, and external agent loops. It runs the identical scan as the Editor window and writes the identical [`preflight-verdict.json`](./verdict-json) — your pipeline gates on the same verdict you see on screen.

## Headless execution

Invoke PreFlight in Unity batchmode using `-executeMethod`:

```bash
Unity -batchmode -quit -projectPath <path-to-project> \
  -executeMethod DecnetGames.PreFlight.Editor.PreFlightHeadless.Run \
  -logFile <path-to-log> \
  -preflightScope Assets \
  -preflightVerdictPath preflight-verdict.json
```

## Command-line arguments

| Argument | Meaning |
| :--- | :--- |
| `-preflightScope <path>` | The project-relative folder to scan. Defaults to `Assets`. |
| `-preflightSafeRepair` | If provided, automatically executes safe repairs before finalizing the scan and verdict. **Default is off** — scan and report only. |
| `-preflightVerdictPath <path>` | Where the machine-readable verdict JSON is written. Defaults to `preflight-verdict.json` at the project root. |

> **Pro Tip:** Leave `-preflightSafeRepair` off in CI until you trust the gate. A scan-only gate that fails the build on findings is already most of the value; automated repair belongs in a step a human reviews, at least at first.

## Exit code contract

PreFlight adheres to a 3-code contract for automation:

| Exit code | Meaning | Automation action |
| :---: | :--- | :--- |
| `0` | **PASS** — Zero open errors in scanned scope. | Proceed to the next pipeline stage or build step. |
| `1` | **FAIL** — One or more open errors detected. | Fail the build or trigger a remediation prompt. |
| `2` | **PreFlight Error** — Unhandled exception or invalid arguments. | Halt the pipeline and check the environment logs. |

Exit code 2 is deliberately distinct from FAIL: a broken *gate* must never look like a broken *project*.

## The verdict file

The headless run writes complete scan metadata to the verdict path — schema, fields and a worked example are documented on the [Verdict JSON](./verdict-json) page. The file contains no absolute drive paths and no environment user names, making it safe to commit or share across build agents.

## Where this fits

- **Pre-commit hook** — scan the changed scope; block the commit on exit 1.
- **CI gate** — scan `Assets` before the build stage; archive `preflight-verdict.json` and the [Markdown report](./markdown-report) as build artefacts.
- **Agent loops** — an AI agent reads the verdict, works the Guided findings from the report's Next Actions, and re-runs the scan: the [re-scan flow](./rescan-flow), automated.

PreFlight itself is deterministic local tooling in all of these: no network calls, no telemetry, nothing leaves the machine — see [What v1 Is Not](./what-v1-is-not) for the exact boundaries.
