# Kame House Nest OAuth information

Public informational pages for Kame House, a personal-use Nest thermostat integration. This repository is deliberately limited to static HTML, CSS, and documentation. It is not an OAuth client, callback endpoint, or Home Assistant configuration repository.

## GitHub Pages

Enable Settings → Pages → Deploy from a branch → `main` → `/ (root)`.

- Homepage: https://gamekommander.github.io/kame-house-nest-oauth/
- Privacy policy: https://gamekommander.github.io/kame-house-nest-oauth/privacy.html

These are the expected URLs after Pages deployment, not a claim that Google has approved them.

## Google OAuth: personal use versus verification

Checked October 13, 2026. Publishing an OAuth app as **In production** is different from Google brand/scope verification or Nest commercial approval.

The current [Home Assistant Nest setup guide](https://www.home-assistant.io/integrations/nest/) recommends a personal-use configuration: fill only the required app name, support email, and developer email; leave optional logo, App domain, and Authorized domains blank; set Audience to External and publish the app as In production. The guide warns that adding optional branding information can trigger verification. [Google's Device Access documentation](https://developers.google.com/nest/device-access/authorize) explicitly states that OAuth API verification is not required for personal use.

**Do not assume a `github.io` page will satisfy Google's verified-domain requirements.** Google [requires an owned, verified domain for reviewed app homepages](https://support.google.com/cloud/answer/15549049) and [recommends using your own domain with shared hosting](https://developers.google.com/identity/protocols/oauth2/production-readiness/policy-compliance). Its current [domain verification guidance](https://support.google.com/cloud/answer/13804266) calls for a DNS-level Domain property, rather than a URL-prefix property. A GitHub Pages repository provides control over page content, not GitHub's DNS. A Search Console HTML file or meta tag is not evidence that Google's OAuth review accepts this domain. If verification is needed, use an owned custom domain, configure its DNS and GitHub Pages mapping, and verify ownership with the Google Cloud project owner's account.

No Google Cloud project was inspected or modified as part of publishing these static files. Acceptance of the GitHub Pages URLs in a particular project's Cloud Console has not been tested. For the documented personal-use route, those optional URLs do not need to be entered at all.

## Remaining manual Google Cloud steps

1. Select the existing Google Cloud project used by the Nest integration. Keep all project IDs and credentials private.
2. In Google Auth Platform → Branding, use `Kame House` and monitored support/developer email addresses. Follow the personal-use guide above and leave optional branding fields blank. If already blocked on verification after adding optional fields, consult the guide's troubleshooting steps and confirm Verification Center shows **Verification not required**.
3. In Audience, confirm **External**, add the owner's Google account as a test user if still Testing, then **Publish app** and confirm **In production**. This removes the Testing-mode seven-day authorization limit; it does not make refresh tokens permanent or expose the owner's home data.
4. Check the OAuth client is a **Web application**. For the standard My Home Assistant flow, retain the exact authorized redirect URI `https://my.home-assistant.io/redirect/oauth`. These public Pages URLs are informational and must not replace that callback. If My Home Assistant was disabled, follow the documented alternate callback setup privately.
5. Confirm the Smart Device Management API and the Device Access project's OAuth client association match the integration. Complete the required Pub/Sub configuration in the current Home Assistant guide. Do not add unrelated permissions merely for these pages; the Nest connection uses `https://www.googleapis.com/auth/sdm.service`.
6. Reauthorize the existing Nest integration after changing from Testing to In production so it receives a fresh authorization. Confirm thermostat access and refresh behavior. An unverified-app notice can still appear for a personal-use app.

If Google actually requires brand/scope verification or the project expands beyond personal use, follow Google's review requirements. These pages alone do not provide verification or commercial Device Access approval.

## Privacy and repository hygiene

Never upload tokens, client secrets, private URLs, IP addresses, Home Assistant backups/configuration, device IDs, room lists, screenshots, or logs. Do not upload the parent workspace. Update the privacy policy if actual data practices change, particularly before offering access to anyone else. The policy acknowledges that private history, logs, and backups can persist; it does not claim that revoking Google access deletes them.
