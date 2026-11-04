# phone-mcp — fleet android activity MCP (fork)

Fork of `hao-cyber/phone-mcp` (upstream, 2026-10-14, 249★) — the most
relevant ADB-native activity MCP as of Nov 2026. Selected via repo-compare
against Droidline (Nov 3, Go agent/server — no MCP), minhalvp/android-mcp-server
(811★, stale 2025-05), droidforge (activities pattern, 0★, stale).
Compare algo: `pens/audit-forks.ts` (signal scoring) + manual feature matrix.

## Why this fork

- `list_app_activities(pkg)` — get app activities over adb (the master-fork
  requirement)
- `launch_app_activity(pkg, activity)` — launch any activity
- `list_installed_apps`, screenshots, media, alarms — full phone control
- MCP-native (FastMCP/Python), stdio + HTTP

## Estate wiring

- Device pin: `ANDROID_SERIAL=10.0.0.77:<port>` REQUIRED — the box sees two
  adb transports (wireless + mDNS tls) and adb errors "more than one
  device/emulator" without it. Port rotates; `estate/pixel-adb-keepalive`
  rescans.
- Venv: `.venv/` (pip install -e .) — PEP 668 blocks system pip.
- Secrets: kryptos keyring only (never commit).

## Known gap

`list_app_activities` only surfaces intent-filter activities (dumpsys
`filter` lines). Full activity sets (e.g. mobilerun's 9 activities) need the
droidforge-style `COMP_RE` parse of `dumpsys package <pkg>` — follow-up.

## Upstream

- upstream: https://github.com/hao-cyber/phone-mcp
- fork: https://github.com/toxicwind/phone-mcp
