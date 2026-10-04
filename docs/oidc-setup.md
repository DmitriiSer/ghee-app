# OIDC (SSO) login setup

Ghee can sign in through the OIDC provider your Mealie server already uses, such as Authentik or Pocket ID. Your provider needs one extra setting before that works.

## Short version

Add this redirect URI to the OIDC client that your Mealie server uses:

```
ghee://oauth/callback
```

Keep the existing Mealie web redirect URIs in place. Nothing changes in Mealie's own configuration.

## Requirements

- Mealie v3.23.0 or newer (required for passkey providers such as Pocket ID)
- Ghee 1.6.0 or newer
- OIDC login already working in the Mealie web app. See the [Mealie OIDC documentation](https://docs.mealie.io/documentation/getting-started/authentication/oidc-v2/).

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

## Other providers

The same step applies to any provider that accepts a custom scheme redirect URI on the client Mealie uses. Authentik and Pocket ID are the two providers tested with Ghee.

Google and Microsoft sign-in do not work with Ghee yet.

## Troubleshooting

- **The provider shows a redirect URI error after you tap the login button.** The URI is missing or does not match. It must be exactly `ghee://oauth/callback`, with no trailing slash.
- **Something else.** [Open an issue](https://github.com/DmitriiSer/ghee-app/issues) and include your Mealie version and provider.
