# Copilot / AI agent instructions for this repository

**Quick summary**
- This repository primarily contains compiled Windows binaries and configuration files for the ProxyTool suite and related utilities. **No source or build files were found** in the workspace; most changes are configuration-level (ini / bat / example files) unless maintainers provide source.

## Quick entry points & run commands ✅
- Main runtime folder: `ProxyTool/`
- Use these launch scripts to run locally:
  - `ProxyTool/Launch_ProxyTool_Advanced.bat`
  - `ProxyTool/Launch_ProxyTool_Optimized.bat`
- Common manual checks:
```bat
netstat -ano | findstr ":26010"      # check ProxyTool port
tasklist /FI "IMAGENAME eq ProxyTool.exe"   # see running process
taskkill /F /IM ProxyTool.exe                 # stop a running process
start "ProxyTool" /HIGH /B ProxyTool.exe    # equivalent to the launcher
```
- Required files checked by the launcher (do not remove).

- Compatibility note: this project references **Proxifier Standard Edition 4.05** (see `Proxifier Standard Edition/please read.txt`).
- Presence of `msvbvm60.dll` and many `.dll` files indicates a legacy/compiled runtime (VB6/C/C++). Source is not present in repo.

## Data formats & concrete examples 💡
- Email import: newline-separated addresses — see `import examples/Email import example.txt`.
- User-Agent import: newline-separated UA strings — see `import examples/UserAgent import example.txt`.
- Referer import: uses a `{||}` delimiter with an HTML snippet, e.g.:
```
google.com{||}<a target="_blank" href="http://whatsmyreferer.com">Click Me</a>
```
  (see `import examples/Referer import example(normal website).txt`).

## Source, builds and edits ⚠️
- **No build system or source files detected.** Do **not** attempt to edit binary `.exe`/`.dll` without source. If a code-level change is requested, **ask maintainers for the canonical source repository** or look for embedded `.git/` dirs (e.g., `ProxyTool/config/.git`) that might contain history.
- Prefer making changes to configuration files (`*.ini`, `*.bat`) or example data (`import examples/`) when appropriate.

## Debugging & validation checklist 🔍
1. Verify required files exist (see required list above).
2. Ensure port 26010 is free: `netstat -ano | findstr ":26010"`.
3. Start via launcher and check with `tasklist` / `taskkill`.
4. Use `Monitor.exe` / `MonitorGUI.exe` (in `ProxyTool/`) to inspect runtime behavior.
5. Collect and include `netstat` / `tasklist` outputs and any log text in PR descriptions or issue reports for reproducibility.

## PR/Change guidance & collaboration (short) 📋
- When proposing config or import-format changes: include exact reproduction steps, which launcher you used, `netstat`/`tasklist` output, and sample input (place under `import examples/`).
- If a source-level change is necessary, request source or raise the ask with maintainers; document the expected change and validation steps.

## Safety & licensing note 


- The `Proxifier Standard Edition/please read.txt` explicitly states no license keys are provided—do not attempt to distribute or request keys. Test network/proxy behavior in an isolated environment.

---
If anything is missing or unclear, tell me which part you want expanded (e.g., more run/debug examples, more examples from `import examples/`, or a checklist for onboarding new contributors). Happy to iterate.