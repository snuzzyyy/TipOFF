# TipOFF — UK NBA app

Native Android Java app with a dark sportsbook-inspired interface. It is built around UK bookmaker prices, decimal odds and GBP stake/return calculations.

## Current features
- NBA fixtures and scores from BALLDONTLIE (requires your own API key).
- Team recent-form comparison using the latest completed games returned by BALLDONTLIE: wins/losses, win rate and average points scored/conceded.
- UK NBA moneyline price display from The Odds API (requires a plan/key that includes the UK region).
- Accumulator builder with locally saved selections, combined decimal odds and potential-return calculations.
- API keys are entered and stored locally in app preferences.
- No invented fixtures or odds. No bet is guaranteed.

## Build an APK
The **TipOFF APK build v3** GitHub Actions workflow runs on pushes to `main` and can also be started manually from the Actions tab. On success, download the `TipOFF-debug-apk` artifact from the workflow run. It contains a debug APK for testing, not a Play Store release.

## API setup
1. Create an account/key at https://www.balldontlie.io/ for NBA games and recent form.
2. Obtain an Odds API key/plan with UK bookmaker region access: https://the-odds-api.com/.
3. Enter the keys in TipOFF > Settings.

The Odds API request explicitly uses `regions=uk` and `oddsFormat=decimal`; the app does not silently substitute US prices. Provider quotas and regional plan restrictions apply.

## Important limitations
- Recent-form figures are descriptive summaries of the returned sample, not calibrated win probabilities or betting recommendations.
- The app does not currently include injury reports, confirmed lineups, player props, historical backtesting or a validated predictive model.
- The scanner displays bookmaker prices; it does not identify guaranteed or proven value bets.
- API keys are stored on-device. Do not distribute a public APK with personal keys embedded; a production release should use a secure backend and protected secret storage.
- Accumulator calculations are mathematical illustrations only. Correlated selections, voids, bookmaker rules and limits can affect settlement.
- For adults 18+ only. Gambling involves risk; never stake money you cannot afford to lose.
