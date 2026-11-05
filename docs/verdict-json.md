---
layout: default
title: Verdict JSON
nav_order: 9
description: "preflight-verdict.json — the machine-readable verdict written at your project root after every scan and repair run: schema, fields, and a worked example."
---

# Verdict JSON — `preflight-verdict.json`
{: .no_toc }

## A verdict your tools can read
{: .no_toc .text-delta }

1. TOC
{:toc}

---

After **every** scan and every repair run — in the Editor window or headless — PreFlight writes **`preflight-verdict.json`** at your project root. It is the machine-readable form of the same verdict you see in the window: your pipeline reads what you read.

The file contains **no absolute drive paths and no environment user names**, so it is safe to commit to version control and to share across build agents and machines.

![The verdict file: status, counts and per-finding entries]({{ "/assets/images/verdict-json.png" | relative_url }})

## Schema

```json
{
  "schemaVersion": "1.0.0",
  "product": "PreFlight",
  "productVersion": "1.0.0",
  "unityVersion": "6000.5.4f1",
  "projectPathHash": "e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
  "timestamp": "2026-11-04T08:00:00.0000000Z",
  "scanScope": "Assets",
  "status": "PASS",
  "summary": {
    "totalFindings": 0,
    "errors": 0,
    "warnings": 0,
    "safeRepairsAvailable": 0,
    "fixedCount": 0
  },
  "findings": []
}
```

| Field | Meaning |
| :--- | :--- |
| `schemaVersion` | Verdict file format version (`1.0.0` in v1). |
| `product` / `productVersion` | What produced the file: PreFlight, and its version. |
| `unityVersion` | The Unity version that ran the scan. |
| `projectPathHash` | A hash identifying the project — deliberately **not** the path itself. |
| `timestamp` | When the run finished (UTC). |
| `scanScope` | The project-relative scope that was scanned (default `Assets`). |
| `status` | **`PASS`** (zero open errors in the scanned scope) or **`FAIL`** (one or more open). |
| `summary.totalFindings` | All open findings in the run. |
| `summary.errors` / `summary.warnings` | The severity split of those findings — on the Harborlight sample's first scan: 12 total, 8 errors, 4 warnings. |
| `summary.safeRepairsAvailable` | Findings currently carrying a Safe fix disposition — the work one [repair run](./repairs) would do. |
| `summary.fixedCount` | Findings repaired by the run that wrote this file (repair runs only). |
| `findings[]` | One entry per finding — see below. |

## The `findings` array

Every finding appears with its **class, path, disposition and status**, so a tool can do more than read the headline — it can, for example, fail a build only on errors, or open a ticket per Guided finding. Two entries in the shape a scan of the Harborlight sample produces:

```json
"findings": [
  {
    "class": "MissingScript",
    "path": "Prefabs/NPC_Patrol.prefab",
    "disposition": "Safe",
    "status": "Open"
  },
  {
    "class": "OrphanedMeta",
    "path": "Textures/pier_weathered_wood.png.meta",
    "disposition": "Safe",
    "status": "Open"
  }
]
```

## What PASS means — and what it does not

`status: "PASS"` means the most recent scan found **zero open findings in the five scanned classes, in the scanned scope**. It does not certify that your gameplay logic, third-party libraries or shaders are correct, and it never claims your project "works" or "builds" — it certifies reference integrity, nothing more. See [What v1 Is Not](./what-v1-is-not).

## Consuming the verdict

- **CI gate:** the headless run's exit code mirrors this file (0 = PASS, 1 = FAIL, 2 = PreFlight error) — most pipelines never need to parse JSON at all. See [Headless & CI](./headless-and-ci).
- **Dashboards and agents:** parse `status` and `summary`; use `projectPathHash` + `timestamp` to match a verdict to the project state it describes.
- **Humans:** the same run also produces the [Markdown report](./markdown-report) — read that one; it has the Next Actions.
