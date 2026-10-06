# OIDC (SSO) login setup

Ghee can sign in through the OIDC provider your Mealie server already uses, such as Authentik, Pocket ID, Google or Microsoft. Your provider needs one extra setting before that works.

## Short version

**Authentik, Pocket ID and similar self-hosted providers:** add this redirect URI to the OIDC client that your Mealie server uses:

```
ghee://oauth/callback
```

Keep the existing Mealie web redirect URIs in place. Nothing changes in Mealie's own configuration.

**Google and Microsoft:** these providers need a separate client for mobile apps, plus two Mealie settings. See [Google](#google) and [Microsoft](#microsoft) below.

## Requirements

- Mealie v3.23.0 or newer (required for passkey providers such as Pocket ID)
- Ghee 1.6.0 or newer
- OIDC login already working in the Mealie web app. See the [Mealie OIDC documentation](https://docs.mealie.io/documentation/getting-started/authentication/oidc-v2/).

Google and Microsoft also need:

- Mealie vX.Y.Z or newer
- Ghee 1.10.0 or newer

## Why the redirect URI is needed

On Mealie v3.23.0 and newer, Ghee opens your provider's login page in the system browser. After you sign in, the provider sends you back to the app through `ghee://oauth/callback`. Providers only redirect to URIs that are registered on the client, so the login fails until this one is added.

## Authentik

1. In the Authentik admin interface, go to **Applications > Providers** and edit the OAuth2/OpenID provider you use for Mealie.
2. Under **Redirect URIs**, add a new entry with the value `ghee://oauth/callback`. Use exact matching, not a regular expression.
3. Save the provider.

## Pocket ID

1. Go to **Administration > OIDC Clients** and open the client you use for Mealie.
2. Add `ghee://oauth/callback` to the client's callback URLs.
3. Save the client.

## Google

Google does not allow app redirect URIs on the web client Mealie uses, so Ghee needs its own client. It has no secret.

1. In the Google Cloud Console project that holds your Mealie web client, create a new OAuth client ID of type **iOS**.
2. Set the bundle ID to `casa.dsen.ghee` and create the client. Copy its client ID. The same client works for Ghee on iOS and Android.
3. Add these settings to your Mealie server, then restart Mealie:

   ```
   OIDC_NATIVE_CLIENT_ID=<the iOS client ID>
   OIDC_NATIVE_CONFIDENTIAL=false
   ```

4. Keep your existing Google web client as `OIDC_CLIENT_ID` and `OIDC_CLIENT_SECRET`. The Mealie web login keeps using it.

You don't add a redirect URI for Google. iOS clients have no redirect URI field, and Ghee uses `casa.dsen.ghee:/oauth/callback` for Google automatically.

If your OAuth consent screen is in testing mode, add each person's Google account as a test user, or they can't sign in.

## Microsoft

Ghee uses the same app registration as the Mealie web login. You add a mobile redirect URI and allow public client flows.

1. In the Microsoft Entra admin center, go to **App registrations** and open the app you use for Mealie.
2. Go to **Authentication > Add a platform > Mobile and desktop applications**. Leave the suggested URIs unchecked, enter `ghee://oauth/callback` as a custom redirect URI, and save.
3. On the same page, set **Allow public client flows** to **Yes** and save.
4. Add these settings to your Mealie server, then restart Mealie:

   ```
   OIDC_NATIVE_CLIENT_ID=<the same Application (client) ID as OIDC_CLIENT_ID>
   OIDC_NATIVE_CONFIDENTIAL=false
   ```

**Personal Microsoft accounts** (Outlook.com, Hotmail) do not send the `email_verified` claim, and Mealie rejects the login until you set `OIDC_REQUIRES_EMAIL_VERIFICATION=false`. This affects the Mealie web login too. The [Mealie email verification docs](https://docs.mealie.io/documentation/getting-started/authentication/oidc-v2/#email-verification) explain the trade-off.

## Other providers

The redirect URI step applies to any provider that accepts a custom scheme redirect URI on the client Mealie uses. Authentik, Pocket ID, Google and Microsoft are the providers tested with Ghee.

## Troubleshooting

- **The provider shows a redirect URI error after you tap the login button.** The URI is missing or does not match. It must be exactly `ghee://oauth/callback`, with no trailing slash.
- **On Android, the sign-in page stays open after you sign in.** You are already signed in. Close the page with **X** to return to Ghee.
- **Something else.** [Open an issue](https://github.com/DmitriiSer/ghee-app/issues) and include your Mealie version and provider.
