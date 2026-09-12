# Urdu Voice Assistant V1.19.0

## Parser Regex Hardening + Version Synchronization

- Fixed Kotlin raw-string regex escaping in command parsers where `\\s`, `\\d`, `\\+`, or `\\b` could prevent intended regex matching.
- Hardened call number detection and contact matching regexes.
- Synchronised Android `versionName` to `1.19.0`.
- Added standalone parser smoke coverage for app search, calls, SMS, WhatsApp, and navigation parsing.

## Verification
- Standalone Kotlin parser smoke test: PASS.
- ZIP integrity: verified after packaging.
- Full Android/Gradle build and device test: not performed because this environment has no Android SDK/Gradle wrapper.
