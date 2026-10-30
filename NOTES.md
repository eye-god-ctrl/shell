---
tags:
  - fork-ledger
  - shell
---

# NOTES.md — shell — the repo decision log

One card per decision/commit, oldest first — append new cards at the bottom.
Cross-repo cards live in the global `../NOTES.md`; empty slots stay bare, no filler.

## 2026-10-30 22:54
* **What:** Upstream sync — `main` fast-forwarded `a3a8fe59` → `b51fdb35c` (30 commits / 296 files) and catch-up-merged into `custom` (`9329c640`, pushed). `custom` now differs from `main` only by our five doc files. Brings: video wallpapers + transitions (#2167/#2180/#2183/#2190/#2193), the wallpaper pause toggle (#2172), the `Multimedia/Visual` stack that replaced `CachingImage` (#2189), `daemons/` + `State/` service modules (#2173/#2174), and the `caelestia` → `caelestia::shell` namespace rename (#2202)
* **Why:** catch the base up before porting midnight's live-wallpaper control layer (R-004) — upstream already shipped the engine, so our port shrinks to the auto-pause rules instead of a ~3,400-line duplicate
* **Taught:** merge-base drift, catch-up merge, upstream-first porting
