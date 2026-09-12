# Urdu Voice Assistant V1.23.0

## Final runtime/setup hardening
- Added Android package-visibility queries for launcher apps and supported app packages.
- Added dynamic launchable-app fallback so generic installed app names can be opened when Android exposes a launcher activity.
- Added microphone permission and SpeechRecognizer availability guards.
- Prevented duplicate/overlapping listen starts with an `isListening` gate and exception-safe `startListening`.
- Expanded common Urdu/Roman Urdu/English time-command coverage.
- Synchronized Android `versionName` to 1.23.0.

## Verification
- Source/static checks: PASS.
- Parser regression smoke tests: PASS.
- ZIP integrity: PASS after packaging.
- Full Android APK/device test: NOT RUN because this environment has no Android SDK/Gradle wrapper/device.
