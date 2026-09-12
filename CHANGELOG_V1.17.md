# Urdu Voice Assistant V1.17.0

## Failure-safe execution boundary
- Added exception-safe coordinator boundary.
- Multi-action engine now exposes ordered execution that stops on the first unhandled/unknown action.
- Remaining actions are never falsely reported as completed.
- Empty commands are rejected safely.

## Verification
- Kotlin source structural checks performed.
- Archive integrity checked.
- Android APK/device test not claimed when SDK/Gradle tooling is unavailable.
