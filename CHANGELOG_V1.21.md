# Urdu Voice Assistant V1.21.0

## Parser & multi-action hardening
- Fixed Kotlin regex escaping in contact normalization, app normalization, and multi-action splitting.
- Fixed `MultiActionCommandEngine` object scope so `execute()` is actually part of the engine.
- Expanded parser smoke coverage for navigation, map search, system actions, and multi-action message boundaries.
- Synced Android `versionName` to `1.21.0`.

## Verification
- Pure Kotlin parser smoke test: PASS.
- Multi-action split smoke test: PASS.
- Source/ZIP structural checks: PASS.
- Full Android APK/device test: NOT RUN (Android SDK/Gradle wrapper unavailable in this environment).
