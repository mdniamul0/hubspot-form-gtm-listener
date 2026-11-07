# Changelog

## v1.1.0 (2026-11-07)

- Works with classic embedded forms (v3, `hsFormCallback`) and forms from HubSpot's new forms editor (v4, `hs-form-event:on-submission:success`).
- v4 submits now send the form ID (it was empty before).
- Only trusts HubSpot messages from your own site or HubSpot domains, and needs a form ID, so other scripts cannot fake a submit.
- Handles HubSpot messages sent as text (JSON strings).
- One push per submit, counted per form, so two forms on one page are both tracked.

## v1.0.0

- First version on mdniamul.com.
