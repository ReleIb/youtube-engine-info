# One engine, multiple channel connections

The website and Google OAuth application describe the shared engine. They do not need to be recreated for each channel. Keep the tool's application name separate from the public YouTube channel names.

## What changes for a new channel

1. Add a unique channel configuration slug in the local engine's `factory/config/channels/` directory.
2. Set that configuration's intended YouTube channel ID and its own production settings.
3. Run the engine's connect flow for that slug. In Google/YouTube authorization, select the intended account or Brand Account channel. Repeat authorization for each channel rather than assuming one token grants every channel.
4. Store the authorization result under that slug and the verified YouTube channel ID. Do not overwrite another channel's tokens.
5. Run a live identity check with that token and compare the returned channel ID with the configured ID. Reject a mismatch before upload.
6. Enable automatic processing for that channel only when its content, voice, publishing settings and connection have been reviewed.

The existing configured `main` channel ID supplied by the owner is `UCieBTZlQekr8xx5lE6Bt6Zw` (currently HUMAN BEFORE on YouTube). The local working name `Money on the Map` is a configuration label and does not rename the YouTube channel. `enabled: false` is a production setting, not evidence of a disconnected OAuth session.

## Requirements for the local engine developer

These are implementation requirements, not a claim that the current engine already implements them:

- Persist tokens per channel connection, together with the OAuth client identity, granted scopes and verified YouTube channel ID.
- Bind the requested slug to a server-side OAuth state record, use a high-entropy one-time state value with an expiry, validate it in the callback, and use PKCE where applicable. Do not trust a bare callback `channel` query parameter as the connection identity.
- Serialize refresh-token updates per connection, preserve a previously stored refresh token when a refresh response omits it, and never let simultaneous refreshes overwrite a newer record.
- Validate the channel identity before saving a new connection and before publishing. A successful token refresh alone does not prove the intended channel was selected.
- Share the existing project's client configuration where appropriate; keep its callback consistent with the actual client type. Google supports desktop loopback callbacks. A web client needs its registered redirect URI to match exactly. Do not switch an existing client type without updating and reauthorizing the engine.
- Keep runtime credentials in private local storage, restrict filesystem access, exclude them from logs and Git, and separate each channel's queued jobs and assets.
- Request only necessary scopes, use offline access when required, and handle `invalid_grant` with a clear per-channel reconnect state rather than repeatedly attempting uploads.
- Share quota accounting across channels in the same Cloud project. Do not create projects to circumvent quotas.
- Provide a way to remove a connection and its stored API data, meet the policy's deletion process, and review stored API data retention and any external AI analysis against Google's rules.

## After switching the application to production

Complete a fresh Google authorization for each channel to replace Testing-era grants. Verify the selected channel ID. Access tokens remain short-lived and should refresh automatically; there is no guarantee that a refresh token lasts forever.

## What this repository changes

It supplies public application information and setup instructions only. It does not modify the local engine, tokens, OAuth clients, channel YAML files or publishing schedule, and it does not enable automatic uploads.
