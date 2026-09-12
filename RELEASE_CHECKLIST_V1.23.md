# V1.23.0 Release Checklist

## Verified here
- Kotlin parser smoke coverage.
- Multi-action routing regression coverage.
- Manifest XML structure and launcher package visibility entries.
- Android versionName consistency.
- No malformed Kotlin raw-string regex escapes in touched source.
- Final ZIP integrity and SHA-256.

## Required on an Android phone
1. Grant microphone permission and test Urdu speech recognition.
2. Test opening WhatsApp, YouTube, TikTok, Instagram, Facebook, Chrome, Calculator and Maps.
3. Test a generic installed app by its visible launcher name.
4. Test microphone tap while already listening.
5. Test phone with no speech-recognition provider available.
6. Test permissions denied for microphone/contacts/call.
7. Test multi-action command and verify execution stops after a blocked action.
8. Test SMS/WhatsApp compose flows before sending.
