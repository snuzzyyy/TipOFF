# TipOFF — UK NBA app

TipOFF is transitioning from a native-only Android app to a hosted web app inside a lightweight Android shell. The hosted UI is designed to update centrally, so normal interface and feature changes will not require a fresh APK install.

## Experience
- Branded welcome screen with a local device profile.
- First-launch, five-step beginner tour covering Games, Match Analysis, UK Odds, Accumulator and News.
- Dark, high-contrast interface with green accents.
- Home, Games, Scanner, Acca, News and Settings sections.

## Current features
- NBA fixtures and scores from BALLDONTLIE (requires your own API key).
- Team recent-form comparison using returned completed games: wins/losses, win rate and average points scored/conceded.
- UK NBA moneyline price display from The Odds API (requires a plan/key that includes UK bookmaker coverage).
- Best returned price shown by outcome with bookmaker name.
- Accumulator builder with locally saved selections, combined decimal odds and potential-return calculations.
- NBA headlines from ESPN RSS.
- API keys entered in Settings and stored in app preferences on the device.

## Hosted app direction\nThe first hosted web app foundation lives in `web/` and is a responsive installable web app. It keeps profile settings, API keys and accumulator selections in the browser's local storage on the device. The Vercel deployment configuration is in `vercel.json`. The Android shell will be switched to this hosted URL after the first deployment is live.\n\n**Update model:** one final Android shell update is required to point the installed app at the hosted web app. After that, changes deployed to the hosted site can appear in TipOFF without reinstalling the Android app. The hosting project must be connected and deployed before the Android shell can safely use its permanent URL.\n\n## Build an APK
The **TipOFF APK build v3** GitHub Actions workflow runs on pushes to `main` and can also be started manually. On success, download the `TipOFF-debug-apk` artifact from the workflow run. It is a debug APK for testing, not a Play Store release.

## API setup
1. Create a BALLDONTLIE account/key for NBA games and recent form: https://www.balldontlie.io/
2. Obtain an Odds API key/plan with UK bookmaker region access: https://the-odds-api.com/
3. Enter the keys in TipOFF > Settings.

The Odds API request explicitly uses `regions=uk` and `oddsFormat=decimal`; the app does not silently substitute US prices. Provider quotas and regional plan restrictions apply.

## Account status
The welcome screen currently creates a local profile name stored on the device. It is not a secure online login, does not verify an email/password and does not sync across devices. A real account system requires an authentication backend and secure session handling.

## Important limitations
- Recent-form figures are descriptive summaries, not calibrated win probabilities or betting recommendations.
- No injury reports, confirmed lineups, player props, historical backtesting or validated predictive model yet.
- The scanner displays bookmaker prices; it does not identify guaranteed or proven value bets.
- API keys are stored on-device. Do not distribute a public APK with personal keys embedded; a production release should use a secure backend and protected secret storage.
- Accumulator calculations are illustrations only. Correlated selections, voids, bookmaker rules and limits can affect settlement.
- Adults 18+ only. Gambling involves risk; never stake money you cannot afford to lose.
## Updates and distribution
The current GitHub Actions output is a debug APK for testing. GitHub Actions builds do not by themselves update an APK already installed on a phone. Android requires each update to be signed with the same persistent release signing identity; a newly generated CI debug signing key is not a safe update channel.

For hands-off updates, the intended production route is Google Play distribution (internal testing first, then production). This requires a Play developer account, a persistent release keystore/signing configuration, a signed Android App Bundle, store listing and policy materials, and Play Console credentials configured as GitHub Actions secrets. Those account credentials and signing materials must be supplied and controlled by the app owner; they must never be committed to this repository. Until that setup is complete, new test builds must be installed manually and Android may reject an update if it was signed with a different key.

## Optional signed Play Store bundle
The workflow always produces a debug APK for device testing. It only produces the `TipOFF-release-aab` artifact when all four release-signing GitHub Actions secrets are configured:

- `ANDROID_KEYSTORE_BASE64` — base64-encoded persistent Java keystore file.
- `ANDROID_KEYSTORE_PASSWORD` — keystore password.
- `ANDROID_KEY_ALIAS` — alias of the signing key inside the keystore.
- `ANDROID_KEY_PASSWORD` — password for that key.

Create the release keystore locally on a trusted computer, keep a secure offline backup, and never commit the keystore or passwords to Git. Convert the keystore file to a single-line base64 value locally before adding it as the `ANDROID_KEYSTORE_BASE64` Actions secret. Add the four values under **Repository Settings → Secrets and variables → Actions**. Do not send the keystore or passwords in chat.

The same release signing identity must be retained for every future update. Losing it can prevent updates to an app distributed outside Google Play. The AAB is only a build artifact; publishing and automatic delivery still require the owner's Google Play Console setup and review. The current workflow does not publish to Google Play automatically.
