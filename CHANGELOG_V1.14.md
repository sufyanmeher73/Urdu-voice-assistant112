# V1.14.0 — Safe Contact Disambiguation

- Added confidence-gap protection to contact resolution.
- Exact/high-confidence unique contacts continue normally.
- Two close strong matches are treated as ambiguous rather than guessed.
- SMS and WhatsApp routing now explain ambiguity instead of silently selecting a contact.
- Direct phone-number calls remain independent of contacts permission.
- No automatic message sending was introduced.
