# UrduVoiceAssistant V1.10.0

## App Search Routing Hardening
- Instagram search routes to the installed Instagram app when possible, with browser fallback.
- Facebook search routes to the installed Facebook app when possible, with browser fallback.
- Google is an explicit searchable target.
- Existing YouTube, TikTok and Maps behavior is preserved.
- Third-party app internals are not automated; routing uses Android intents and supported web URLs.
