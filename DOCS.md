# DOCS.md — the story of the shell fork
Non-coder-friendly first, "For devs" inside each chapter. See ../playbooks/docs-fold.md.
`Last folded: 2026-10-30 22:54 — upstream sync`

## **Chapter 1 — Upstream sync (2026-10-30)**
**What it is.** The shell fork was brought back level with upstream Caelestia: 30 new upstream commits (296 files) were merged into this repo's `custom` branch. No fork-specific code changed — this fork still only adds documentation — but the upstream code underneath moved forward, and it brought a headline feature with it.

**Why it exists.** Upstream shipped **video wallpapers** (set an `.mp4` as your desktop background, with shader transitions between wallpapers) plus a **pause toggle** in the quick-toggles panel. We wanted that feature; the alternative — hand-copying it from the midnight fork — meant ~3,400 duplicated lines that break on every future upstream release. Catching up first means the engine comes free and we only build the small extra layer (auto-pause on battery, auto-pause when a window covers the wallpaper, animated GIFs) — roadmap item R-004.

**How it works (non-coder version).** Two branches: `main` is a pure copy of upstream and is never edited; `custom` is what you actually use — upstream plus this fork's changes. The sync slid `main` forward, merged it into `custom` as one clearly-labelled commit, then pushed to GitHub.

**For devs.** Merge commit `9329c640`; upstream range `a3a8fe59..b51fdb35c`. Added: `plugin/src/Caelestia/Multimedia/` (Visual.qml, visualsource.cpp, imagecache, ktxencoder) from #2167; `components/widgets/WallpaperImpl.qml` renders `Visual { playing: PersistentState.wallpaperPlaying }`; `plugin/src/Caelestia/State/` and top-level `daemons/` from #2173/#2174; `CONFIG_ENUM_PROPERTY(WallpaperTransition, …)` in `plugin/src/Caelestia/Config/backgroundconfig.hpp` + `enums.hpp`. **Deleted:** `components/images/CachingImage.qml` and `plugin/src/Caelestia/Images/{iutils,imagecacher,cachingimageprovider}` (#2189). Renamed: C++ namespace `caelestia` → `caelestia::shell` (#2202, 156 files). New dependency: `qt6-multimedia`.

**How it differs from upstream.** Only the five fork documentation files (`AGENTS.md`, `CLAUDE.md`, `DOCS.md`, `NOTES.md`, `VERSIONS.md`). Upstream touches none of them, so future syncs should stay conflict-free.

**Risks / how to undo.** The new rendering path uploads KTX textures (`GL_BC3`) and decodes video through QtMultimedia — it has never run on this machine. Undo is `git revert -m 1 9329c640`, a normal commit; history is never rewritten. Note the deleted `CachingImage` stack: any plan still mentioning midnight's old C++ image helpers is stale.

**What was verified, and what wasn't.** Verified: fast-forward clean, `git merge-tree` conflict preview clean, `custom` contains upstream's tip, `diff main..custom` shows only the five doc files, zero conflict markers, local == GitHub. **Not verified:** build, video playback, pause toggle, GPU behaviour — all HUMAN-ONLY in the VM (`playbooks/vm-verify.md` + `playbooks/gpu-verify.md`), still open as P0-6.

**You learned:** *merge-base drift*, *catch-up merge*, *upstream-first porting* (see the global Toolbox in `../DOCS.md`).
