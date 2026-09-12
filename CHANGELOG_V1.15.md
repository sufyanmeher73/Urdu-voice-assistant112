# Urdu Voice Assistant V1.15.0

## Context-aware multi-action splitting

- Hardened `MultiActionCommandEngine.split()` so common separators do not blindly break message/search content.
- Message and WhatsApp segments can preserve natural `aur`/`and` text when the following segment is not a recognizable action.
- Added lightweight action-boundary detection using the existing parsers.
- Preserved existing action classification and execution routing.

## Verification

- Source-level structural checks performed.
- ZIP contents and checksum verified.
- Android APK/device testing is not claimed when the Android SDK/Gradle environment is unavailable.
