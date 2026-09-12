# Urdu Voice Assistant V1.25.0

## V1.25.0 — Stabilization pass (this build)
- **Fixed a compile-breaking bug**: `MainActivity` called a non-existent
  `ContactResolver.find(...)` with fields (`.number`, `.name`) that don't
  exist on `ContactMatch`. That dead legacy call-handling branch was
  removed entirely; calling now always goes through `CallCommandParser`
  + `CallRouter`, which already has correct contact resolution and
  permission handling.
- Removed unused dead code: `CommandEngine.kt` and `CapabilityRegistry.kt`
  (superseded by `MultiActionCommandEngine` + the `*CommandParser`
  classes, but never deleted).
- Removed duplicate/unreachable handler methods in `MainActivity`
  (`handleAppSpecificSearch`, `handleSmsCommand`, `handleWhatsAppCommand`,
  `handleNavigationCommand`, `handleMapSearchCommand`,
  `handleCommonAppOpen`) that duplicated `CommandExecutionCoordinator`.
- Added automatic command retry: when a command triggers a permission
  request (mic, contacts, call), granting the permission now re-runs the
  same command instead of requiring the user to repeat it.
- Moved smoke tests from a loose `test/` folder (plain `main()` scripts,
  never actually run by Gradle) into real JUnit tests under
  `app/src/test/java/...`, wired `junit:junit` into `app/build.gradle.kts`,
  and added a `gradle test` step to the CI workflow before `assembleDebug`.
- Added a `release` build type with `minifyEnabled` + ProGuard rules, and
  pinned Java/Kotlin toolchain to 17 to match the CI workflow.

## V1.18.0

V1.15.0 adds safe contact disambiguation: contact-based call/SMS/WhatsApp routing refuses to guess when two strong contact matches are too close. Direct phone-number calling remains unaffected.

## Verification
- Kotlin source consistency checks: PASS
- Required routing/permission classes present: PASS
- ZIP integrity: PASS after packaging
- Android APK/device test: not claimed; this source environment does not include an Android SDK/Gradle wrapper.

# Urdu Voice Assistant — V1.12.0

A native Android starter app for a personal Urdu/Roman-Urdu voice assistant.

## Included
- Urdu speech recognition (`ur-PK`)
- Urdu text-to-speech response
- App launching for common apps
- Google/web search
- Time/date response
- Camera/settings/file picker actions
- Phone call intent with permission
- WhatsApp launch flow
- Simple command normalization

## Important Android limitation
Third-party apps such as WhatsApp/TikTok control their own internal UI. An Android app cannot universally and silently perform every internal action. Deep links, official APIs, intents, or (where appropriate and user-enabled) Accessibility services are required for deeper automation.

This V1 deliberately avoids pretending unsupported actions are completed.

## Build
Open this folder in Android Studio, let Gradle sync, then run on an Android device.

Target SDK: 35
Min SDK: 26
Application ID: com.edusphere.urduassistant

## Next professional phase
- Offline/online Urdu NLU layer
- Contact-name resolution
- App capability registry
- Deep-link handlers
- Optional user-enabled Accessibility automation
- Confirmation/safety engine
- Background hotword service
- Command history/settings
- More Urdu + Roman Urdu variants
- Full device test matrix


## V1.1.0 upgrade
- Separated natural-language parsing into `CommandEngine`
- Added Urdu/Roman Urdu/English alias normalization
- Added structured parsed-command types
- Added capability registry for transparent support/confirmation rules
- Improved parsing for search, message, call and app commands

The parser is intentionally separated from Android UI so it can later be backed by a stronger Urdu NLU/LLM layer without rewriting the action layer.

## V1.2.0 upgrade
- Added contact-name resolution from Android Contacts
- Added real phone-call intent by contact name/number
- Added WhatsApp text sharing flow with user review before sending
- Added SMS permission declaration for the next messaging layer

## V1.3.0 — App-specific Search & Deep Links
- Added centralized `AppActionRouter`.
- Added YouTube, TikTok, Google and Maps search routing.
- Tries the relevant installed app first where a package/deep-link is available.
- Falls back to the web when the target app is unavailable or rejects the deep link.
- Added Roman Urdu/Urdu command patterns for app-specific search.
- Removed unused direct `SEND_SMS` permission; SMS compose remains a safer later capability.
- This source package has not been APK-compiled in this environment because Android SDK/Gradle are unavailable here.

## V1.5.0 — Contact Resolution + WhatsApp Messaging
- Improved contact matching with exact/token/partial scoring.
- Added dedicated WhatsApp command parsing.
- Added phone-targeted WhatsApp message routing via wa.me when a contact is resolved.
- Falls back to WhatsApp text share when no contact target is provided.
- User review/send remains required; silent third-party-app sending is not claimed.
- APK/device testing is not verified in this environment because Android SDK/Gradle are unavailable.

## V1.6.0 — Maps & Navigation
- Added Google Maps place search routing.
- Added navigation/directions commands.
- Tries the Google Maps app first and falls back to web Maps.
- Added Roman Urdu and Urdu navigation command patterns.
- Does not claim current GPS location unless the device/location APIs are explicitly added later.
- APK/device testing is not verified in this environment because Android SDK/Gradle are unavailable.

## V1.7.0 — Common App Actions
- Added centralized common-app launcher.
- Added Urdu/Roman Urdu/English open-app commands.
- Added shortcuts for WhatsApp, YouTube, TikTok, Instagram, Facebook, Chrome, Calculator and Maps.
- Uses Android package launch intents and reports when an app is unavailable.
- Does not claim arbitrary internal third-party UI automation yet.
- APK/device testing is not verified in this environment because Android SDK/Gradle are unavailable.

## V1.8.0 — Multi-Action Command Engine
- Added sequential multi-command planning for common conjunctions such as "aur", "phir", and "and".
- Added action classification for app open, search, call, SMS, WhatsApp, navigation, time and system actions.
- Added a coordinator that reuses existing safe routers.
- Unknown segments prevent multi-action execution rather than guessing.
- Does not attempt hidden/background UI automation.
- APK/device testing is not verified in this environment because Android SDK/Gradle are unavailable.


## V1.9.0 — Generic App Search Routing
- Added `AppSearchCommandParser` for reusable app-specific search parsing.
- Supports YouTube, TikTok, Instagram, Facebook and Maps aliases in English, Roman Urdu and Urdu.
- Added app-search handling to the multi-action execution coordinator.
- Kept third-party app automation honest: search is routed through supported deep links/web fallbacks; no claim of hidden UI automation.
- Added an explicit `app_search` capability to the capability registry.
- Android APK/device testing remains unverified here when the Android SDK/Gradle toolchain is unavailable.


## V1.10.0 — App Search Routing Hardening
- Added Instagram and Facebook app/web search routing.
- Added Google as an explicit searchable target.
- Preserved safe web fallback when the target app is unavailable.
- Third-party app internals are not automated; actions use supported intents/URLs.


## V1.11.0 — Unified Command Routing
- Main voice execution now uses the shared multi-action engine before legacy fallbacks.
- App-specific search/open, navigation, map search, SMS and WhatsApp commands use the same coordinator path.
- Fixes a routing gap where newer parsers existed but the microphone entry point could bypass them.
- Multi-action commands now execute through the shared coordinator from the actual voice flow.
- Android APK/device testing remains unverified when the Android SDK/Gradle toolchain is unavailable.


## V1.12.0 — Permission-Aware Call Routing
- Added a dedicated call command parser for phone numbers and contact names.
- Unified multi-action execution now correctly routes CALL actions instead of classifying them without an executor.
- Contact and phone-call permissions are checked before querying contacts or starting a call.
- Permission requests are issued through the hosting Activity when available; the assistant asks the user to repeat the command after granting permission.
- Direct phone calls remain confirmation-sensitive in the capability registry; no silent permission bypass is attempted.
- Android APK/device testing remains unverified when the Android SDK/Gradle toolchain is unavailable.

## V1.13.0 — Permission-Safe Contact Commands
- Centralized contact permission guard for SMS, WhatsApp contact lookup, and calls.
- Avoids requesting READ_CONTACTS for direct phone-number calls.
- Protected contact queries now return a clear permission/retry response instead of risking a SecurityException.
- APK/device testing remains unverified without Android SDK/Gradle.


## V1.17.0
Failure-safe multi-action execution boundary added.


## V1.18.0 — Strict Execution Result Semantics

Blocked or failed call/contact actions now return an unhandled result. Permission requests, missing contacts, ambiguous contacts, and failed call launches therefore stop a multi-action sequence instead of being falsely counted as completed.


## Current source
V1.23.0 includes final runtime/setup hardening and source-level regression coverage. See `CHANGELOG_V1.23.md` and `RELEASE_CHECKLIST_V1.23.md`.


## Phone-only cloud build

See `CLOUD_BUILD_GUIDE.md`. A GitHub Actions workflow is included at `.github/workflows/android-apk.yml` to build the debug APK without a local Android Studio installation.
