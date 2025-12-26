# Copilot / AI agent instructions for this repository

**Quick summary**
- This worktree contains repository metadata and guidance for the ProxyTool distribution; **no application source or build system is present** here. The repo snapshot primarily targets runtime/configuration and example data; compiled binaries and configuration artefacts are expected to live in a `ProxyTool/` runtime folder (not always present in this worktree).

## What an agent needs to know (high level) ✅
- This project is a **compiled distribution** (Windows executables + INI/BAT configs). The code that built those artifacts is not in this workspace — ask maintainers for the canonical source repo when a code change is required.
- Configuration-driven design: behavior and routing are controlled by `.ini` files, `.bat` launch scripts, and example input files under `import examples/`.
- Common runtime port: **26010** (used internally; check `ns.ini` if present).

## Key files & concrete examples 🔎
- Expected runtime artifacts (when present): `ProxyTool/Launch_ProxyTool_Advanced.bat`, `ProxyTool/Launch_ProxyTool_Optimized.bat`, `ProxyTool.exe`, `Monitor.exe`, `MonitorGUI.exe`.
- Required files the launcher checks (do not remove): ``_spd.ppx``, ``filter.ini``, ``ns.ini``.
- Process mapping example: `ProxyTool/filter.ini` maps `ps1..ps8` → process names (examples: `Client.exe`, `forward.exe`, `GuiHelper.exe`, `Socket.exe`). Keep names consistent if you rename items.
- Import format examples (concrete files referenced in this worktree):
  - `import examples/Email import example.txt` (newline-separated addresses)
  - `import examples/UserAgent import example.txt` (newline-separated UA strings)
  - `import examples/Referer import example(normal website).txt` (uses `{||}` delimiter for HTML snippet)

## Patterns & repository conventions ⚖️
- Do not modify binaries (`*.exe`, `*.dll`) in-place — this repo is a binary distribution. Any change requiring source-level edits must be done in the canonical source repo.
- Preferred edit surface: configuration (`*.ini`, `*.bat`) and `import examples/`. These are the safest, testable changes here.
- Keep configuration and launcher scripts consistent: changes to `filter.ini` (process name keys) usually require corresponding launcher or readme updates.
- This snapshot contains legacy runtime artifacts (e.g., `msvbvm60.dll`) — expect VB6 / older C/C++ components.

## Developer workflow & validation steps 🔧
- Common debug commands (Windows CMD/PowerShell):
  - Check port: `netstat -ano | findstr ":26010"`
  - Verify process: `tasklist /FI "IMAGENAME eq ProxyTool.exe"`
  - Stop process: `taskkill /F /IM ProxyTool.exe`
  - Start manually (if binaries present): `start "ProxyTool" /HIGH /B ProxyTool.exe`
- Use `Monitor.exe` / `MonitorGUI.exe` (if present) to inspect runtime activity and validate config changes.
- When validating changes, collect and attach `netstat`/`tasklist` output and any runtime logs to your PR or issue to make reproductions easier.

## PR checklist for config/data changes ✅
- Describe the exact reproduction steps and the launcher used.
- Attach sample input files (place under `import examples/` with a clear filename and short README if needed).
- Include `netstat` / `tasklist` / Monitor output showing the observed behavior and the expected behavior.
- Do not commit modified binaries; instead, document required code changes and ask maintainers for source access.

## Guidance for AI agents / Copilot-style tasks 🤖
- When asked to "fix a bug" or "change behavior": first confirm whether the change requires source code or a config fix. If source is required, stop and request the canonical source repo and a point of contact.
- When editing configs: make minimal, reversible edits, include a short validation snippet (commands to run to verify), and add example inputs under `import examples/` for regression testing.
- Avoid adding secrets or license keys; this repository references **Proxifier Standard Edition 4.05** — do not attempt to supply or store keys here.

## Where to look for more context 🧭
- If contributors mention `ProxyTool/config/.git` or similar, that may point to a history-containing subrepo — ask maintainers to share it.
- If you need to run components not present in this snapshot, request a runtime bundle (the `ProxyTool/` folder) or direct access to a machine that has the binaries installed.

---
If anything here is unclear or you need more examples (e.g., a sample `filter.ini` snippet, a template for a config PR, or a short troubleshooting script), tell me what to add and I will iterate.