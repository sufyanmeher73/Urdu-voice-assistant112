# V1.18.0 — Strict Execution Result Semantics

- Corrected multi-action execution so blocked/failed call and contact-dependent actions return `handled=false`.
- Permission requests no longer count as completed actions.
- Missing/ambiguous contacts no longer count as successful actions.
- Failed call launch now correctly reports an unhandled result, so later actions are not executed.
- Preserves the V1.17 stop-on-first-unhandled execution boundary.

## Verification
- Source static consistency checks: PASS
- ZIP integrity: PASS after packaging
- Android APK/device test: not claimed; Android SDK/Gradle tooling is unavailable in this environment.
