# Privacy Policy

**Ghee — Mealie Companion App**
Last updated: February 22, 2026

## Who We Are

Ghee is developed by Dmitrii Serikov, an independent developer. You can contact us at [github.com/DmitriiSer/ghee-app](https://github.com/DmitriiSer/ghee-app/issues).

## Overview

Ghee is a mobile app that connects to your self-hosted [Mealie](https://mealie.io/) recipe server. Your recipe and shopping list data stays on your own server — we do not operate any backend servers and do not have access to your data.

## Data We Collect

### Analytics & Crash Reporting

We use **Firebase Analytics** and **Firebase Crashlytics** (provided by Google) to understand how the app is used and to fix crashes. This includes:

- **Usage events**: which features you use (e.g., opening a recipe, downloading for offline, starting cook mode). These events do not include the content of your recipes or shopping lists.
- **Crash reports**: technical information about app errors, including device model, OS version, and stack traces.
- **User identifier**: your Mealie user ID is associated with analytics and crash data to help diagnose user-specific issues.

Firebase may also collect standard device and usage information as described in [Google's privacy policy](https://policies.google.com/privacy) and [Firebase's data processing terms](https://firebase.google.com/terms/data-processing-terms).

**Legal basis (GDPR):** Legitimate interest — we use analytics to improve app stability and user experience. You can disable analytics and crash reporting from within the app.

### Data Stored on Your Device

The following data is stored locally on your device using platform-provided encrypted storage (Keychain on iOS, EncryptedSharedPreferences on Android):

- Your Mealie server URL and authentication tokens
- Your user profile information (name, email) as provided by your Mealie server
- App preferences (theme, display settings)

When you download recipes for offline use, recipe data and images are stored in the app's local storage on your device.

None of this data leaves your device except to communicate with your own Mealie server.

## Data We Do NOT Collect

- We do not collect your name, email, or contact information on our servers
- We do not collect location data
- We do not access your camera, microphone, or contacts
- We do not serve ads or share data with advertisers
- We do not sell any data to third parties

## Your Mealie Server

All recipe and shopping list data is transmitted directly between the app and your self-hosted Mealie server. We have no access to your server and cannot see your recipes, shopping lists, or any other data stored there.

## Third-Party Services

| Service              | Purpose         | Privacy Policy                                                  |
| -------------------- | --------------- | --------------------------------------------------------------- |
| Firebase Analytics   | Usage analytics | [Google Privacy Policy](https://policies.google.com/privacy)    |
| Firebase Crashlytics | Crash reporting | [Firebase Privacy](https://firebase.google.com/support/privacy) |

Analytics data may be transferred to and processed on Google's servers in the United States or other countries where Google operates. Google processes this data under their [data processing terms](https://firebase.google.com/terms/data-processing-terms) and is obligated to protect your data in accordance with their privacy policies.

## Data Security

Data transmitted to your Mealie server uses the connection settings you configure (HTTPS where applicable). See "Data Stored on Your Device" above for how local data is protected.

## Data Retention

- Analytics and crash data is retained by Firebase according to [Google's data retention policies](https://firebase.google.com/support/privacy).
- Logging out deletes your stored credentials (tokens, server URL, username, and profile). Offline downloaded recipes and app preferences remain on-device until you uninstall the app.

## Your Rights

Depending on your location, you may have the right to:

- **Access** the personal data we hold about you
- **Request deletion** of your data
- **Object** to data processing based on legitimate interest
- **Lodge a complaint** with your local data protection authority

Since we do not maintain user accounts or databases, most of your data is on your own device (which you control). If you contact us with a deletion request, we will remove your associated analytics data from Firebase.

## Children's Privacy

Ghee is not directed at children under 13. We do not knowingly collect personal information from children.

## Changes to This Policy

We may update this policy from time to time. Changes will be posted on this page with an updated date.

## Contact

If you have questions about this privacy policy, please open an issue at [github.com/DmitriiSer/ghee-app](https://github.com/DmitriiSer/ghee-app/issues).
