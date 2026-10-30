# VERSIONS.md — shell
## Upstream sync ledger
- Last synced upstream SHA: `b51fdb35ca7a14ac5a49e0d94fc5de2d79756aed` — date: 2026-10-30
- Adopted upstream commits: **all 30** (`a3a8fe59..b51fdb35c`) — adopted wholesale via catch-up merge `9329c640`; per-commit verdicts in `../reports/sync-2026-10-30.md`
- Skipped upstream commits (with reason): _(none)_
## What each merge into custom brings
| Date | custom SHA | stack tag | What it brings |
|---|---|---|---|
| 2026-10-30 | `9329c640` | — | Upstream catch-up merge (`a3a8fe59` → `b51fdb35c`, 30 commits / 296 files): video wallpapers + transitions (#2167, #2180, #2183, #2190, #2193), wallpaper pause toggle (#2172), new `plugin/src/Caelestia/Multimedia/` stack replacing `CachingImage` (#2189), `daemons/` + `plugin/src/Caelestia/State/` service refactor (#2173, #2174), C++ namespace `caelestia` → `caelestia::shell` (#2202), lock-screen Ctrl+U (#2159). New dependency: `qt6-multimedia` |
