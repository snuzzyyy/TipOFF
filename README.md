# TipOFF — UK NBA app

A native Android NBA companion built around UK bookmaker prices, decimal odds and GBP calculations.

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

## Build an APK
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
