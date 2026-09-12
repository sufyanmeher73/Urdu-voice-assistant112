# Urdu Voice Assistant — V1.13.0

## Permission-Safe Contact Commands
- Added a centralized `ContactPermissionGate` for contact-backed commands.
- SMS-to-contact now checks `READ_CONTACTS` before querying contacts.
- WhatsApp-to-contact now checks `READ_CONTACTS` before resolving a contact.
- Phone-call contact lookup reuses the same permission guard.
- Direct phone-number calls do not request contact access unnecessarily.
- Missing permission returns a clear retry instruction instead of attempting a protected contacts query.
- Existing compose/review behavior for SMS and WhatsApp is preserved.

## Verification
- Kotlin/source structural checks passed.
- ZIP integrity verified after packaging.
- Android APK/device execution is not claimed because this environment has no Android SDK/Gradle toolchain.
