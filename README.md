# HubSpot Form GTM Event Listener

**Free Google Tag Manager listener for HubSpot form tracking.** It fires one `hubspot_form_submit` event when someone submits a HubSpot form embedded on your website, for both the classic embed and forms built in HubSpot's new forms editor, so you can track HubSpot form submissions in GA4, Google Ads, Meta Pixel and any other tag.

![HubSpot Form GTM Event Listener](docs/banner.png)

**Full guide, install video and copy button:** https://mdniamul.com/gtm-event-listeners/hubspot-form-gtm-listener/

---

## What it does

HubSpot tells your page when a form is sent successfully:

- **Classic embed (v3):** a `hsFormCallback` message with `eventName: 'onFormSubmitted'`
- **New forms editor (v4):** the `hs-form-event:on-submission:success` event

This listener catches both and pushes:

```js
{
  event: 'hubspot_form_submit',
  form_id: '908c5d9e-5f25-466e-bb02-35f2f363b29d',
  page_path: '/contact-us/'
}
```

Built-in safety:

- Fires only after HubSpot confirms the submit, never on a click that fails validation
- Only trusts HubSpot messages from your own site or HubSpot domains, and needs a real form ID
- Ignores empty, broken or unrelated messages from other iframes and extensions
- One push per submit, counted per form, so two forms on one page both work

## Install in 6 steps

1. **Embed the HubSpot form on your page.** HubSpot → Marketing → Forms → your form → Share → Embed code. Paste it into your page (in Elementor use the HTML widget).
2. **GTM → Tags → New → Custom HTML.** Paste [`hubspot-form-gtm-listener.html`](hubspot-form-gtm-listener.html). Trigger: **All Pages**.
3. **Triggers → New → Custom Event**, event name `hubspot_form_submit`.
4. **Variables → New → Data Layer Variable**: `DLV - form_id` → `form_id`. Use it to track one form only.
5. Fire your **GA4 event** (for example `generate_lead`), **Google Ads conversion** or **Meta Pixel** `Lead` event on that trigger.
6. **Preview**, submit a test lead, check the event in Tag Assistant, then **Publish**.

## Files

| File | What it is |
|---|---|
| `hubspot-form-gtm-listener.html` | Ready to paste into a GTM Custom HTML tag |
| `hubspot-form-gtm-listener.js` | Same code without the `<script>` tags |
| `examples/sample-datalayer-output.json` | What the push looks like |

## Videos

- Install the free code: https://mdniamul.com/gtm-event-listeners/hubspot-form-gtm-listener/#install-video
- What the advanced version collects: https://mdniamul.com/gtm-event-listeners/hubspot-form-gtm-listener/#advanced

## Step-by-step guides

- [HubSpot form submission tracking in GA4 with GTM](https://mdniamul.com/blog/hubspot-form-submission-event-tracking-in-ga4-with-gtm/)
- [HubSpot landing page form tracking for Google Ads](https://mdniamul.com/blog/hubspot-landing-page-form-submission-google-ads-conversion-tracking/)
- [Google Ads offline conversions with HubSpot CRM](https://mdniamul.com/blog/google-ads-offline-conversion-tracking-google-sheets-hubspot-crm/)

## Need more data? Advanced version

The free code tells you a form was sent. The **advanced version** also sends the lead's SHA-256 hashed email, name, phone and address, the form version, the HubSpot conversion ID and `hubspotutk` cookie for CRM matching, UTM values, 17 ad click IDs, first-party cookies (`_ga`, `_fbp`, `_fbc`, `_gcl_au` and more), visitor location and a unique `event_id`. Ready for Google Ads Enhanced Conversions, Meta CAPI, TikTok Events API and server-side GTM.

It comes with a setup video, a PDF guide and a GTM import file in your client portal. The code starts from $89, and setup packages are available:

- Prices: https://mdniamul.com/gtm-event-listeners/hubspot-form-gtm-listener/#pricing
- WhatsApp: https://api.whatsapp.com/send?phone=8801776485758
- Book a call: https://calendly.com/mdniamul
- All listeners: https://mdniamul.com/gtm-event-listeners/

Want it done for you? See my [HubSpot form conversion tracking service](https://mdniamul.com/hubspot-form-conversion-tracking-services/) and the [HubSpot conversion tracking specialist](https://mdniamul.com/hubspot-conversion-tracking-specialist/) page.

## Troubleshooting

- **No event:** GTM is not on the page with the form (common on HubSpot-hosted landing pages), or the tag is paused.
- **Two events:** an older listener is still live. Keep one.
- **Check the raw signal:** classic forms `window.addEventListener('message', e => console.log(e.origin, e.data))`, new editor forms `window.addEventListener('hs-form-event:on-submission:success', e => console.log(e.detail))`. Then submit a test lead.

## About

Built by **[MD Niamul](https://mdniamul.com)**, GoHighLevel & AI Agent Automation, Marketing Attribution and Server-Side Tracking Specialist. Founder of Digital Soldier Agency and official Stape partner.

[Website](https://mdniamul.com) · [Free GTM listeners](https://mdniamul.com/gtm-event-listeners/) · [Book a call](https://calendly.com/mdniamul) · [LinkedIn](https://linkedin.com/in/mdniamul)

## License

MIT. Free to use on your own and your clients' sites. See [LICENSE](LICENSE).
