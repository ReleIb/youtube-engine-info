# UBT Stories / YouTube Engine — public application information

Static public pages for the locally operated video engine. The current OAuth display name is **UBT Stories**; **YouTube Engine** describes the shared tool, not a specific channel. This site can describe multiple channels owned or managed by the same operator. A new channel does not need a new information website or repository.

## Enable GitHub Pages once

In this repository open **Settings → Pages**:

1. Source: **Deploy from a branch**.
2. Branch: **main**.
3. Folder: **/(root)**.
4. **Save**. Wait for the Pages deployment to finish and open the actual site URL shown by GitHub.

Expected URLs after successful deployment (not a claim that deployment is already active):

- Home: https://releib.github.io/youtube-engine-info/
- Privacy: https://releib.github.io/youtube-engine-info/privacy.html
- Terms: https://releib.github.io/youtube-engine-info/terms.html

## Google Auth Platform → Branding

Use the **Youtube Engine 2026** project that the local uploader actually uses. Keep the existing OAuth client credentials and callback unless inspection shows they are incorrect.

| Google Console field | Value after Pages is live |
| --- | --- |
| Anwendungsname | UBT Stories |
| Nutzersupport-E-Mail | refikrele@gmail.com |
| Startseite der Anwendung | https://releib.github.io/youtube-engine-info/ |
| Link zur Datenschutzerklärung der Anwendung | https://releib.github.io/youtube-engine-info/privacy.html |
| Link zu den Nutzungsbedingungen der Anwendung | https://releib.github.io/youtube-engine-info/terms.html |
| Kontaktdaten des Entwicklers | refikrele@gmail.com |

If an authorized domain is requested, register the site host **releib.github.io**. Google validates domain rules and can require domain-ownership proof for verification. Do not enter `github.com`, `127.0.0.1`, a URL path, or somebody else's domain as the public app domain. If domain validation fails, follow the actual Console error rather than substituting an unrelated address. A custom domain may be needed if Google's ownership verification requires it.

Save Branding, then **Zielgruppe → App veröffentlichen**. Confirm that **Veröffentlichungsstatus** becomes **In Produktion**. Production publishing and Google verification are distinct; personal-use apps may qualify for a verification exception. Publishing does not bypass YouTube API quotas, upload audits or Google policies.

Reconnect each local channel once after changing to production and retain a new refresh token. Confirm live channel identity before allowing uploads. A one-hour access-token expiry is normal and is separate from the seven-day Testing refresh-token limit. Refresh tokens can still expire or be revoked for other reasons.

## Multiple channels

See [MULTICHANNEL.md](MULTICHANNEL.md). These public pages do not implement the engine's connection logic. Each channel needs its own validated authorization record. Do not duplicate Cloud projects to evade quota limits.

## Owner review before relying on the published policy

The text is based on the supplied local dashboard and described workflow; the engine source was not available for inspection. Confirm that actual storage, deletion handling, backup handling, AI-provider transfers and Google Limited Use obligations match the policy. In particular, implement the seven-day verified deletion-request process and check the handling of analytics data before passing it to an external analysis provider. If a provider would use Google user data to train a generalized model, do not make that transfer. If implementation differs, correct either the behavior or the policy before publishing the OAuth app.

## Site contents

- `index.html`: shared application overview and contact.
- `privacy.html`: privacy policy, YouTube data access, external providers, revocation and deletion.
- `terms.html`: terms with YouTube Terms of Service link.
- `styles.css`: local responsive styling. No JavaScript, third-party fonts, trackers or build dependencies.
- `.nojekyll`: serve static files directly.

Only public information belongs in this repository. OAuth tokens, credentials, engine configuration, local databases and private analytics must remain outside it. A `.gitignore` is included as an extra guard; it does not remove secrets already committed elsewhere.

Operator: Refik Ibrahimović / ReleIb · refikrele@gmail.com
