# V1.12.0 — Permission-Aware Call Routing

- Added dedicated `CallCommandParser` for Roman Urdu/Urdu/English call commands.
- Added `CallRouter` with READ_CONTACTS and CALL_PHONE permission checks.
- Fixed unified coordinator gap where `CALL` was classified but not executable.
- Multi-action call segments now route through the same coordinator as other actions.
- No permission bypass or silent call behavior is claimed.
