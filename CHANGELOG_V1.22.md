# Urdu Voice Assistant V1.22.0

## Execution safety & routing hardening
- MainActivity now treats coordinator-recognized commands as terminal, preventing legacy fallback handlers from double-executing a command.
- Call commands are explicitly included in the unified coordinator routing gate.
- Multi-action execution now stops at the first blocked/failed action and reports skipped actions instead of continuing blindly.
- Added routing regression coverage for system, call, app-open, and message-boundary multi-action plans.

## Verification
- Source structure checks: PASS.
- Regression test source added: PASS (requires Android-independent parser test harness execution).
- ZIP integrity: verified after packaging.
- Full Android APK/device test: NOT RUN (Android SDK/Gradle wrapper unavailable).
