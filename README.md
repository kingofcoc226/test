# F1 Timer Sports (Android)

Android port of the F1 Timer Desk Widget. Pure-black AMOLED UI, live clock, weather, the F1 schedule in your time zone
(default Asia/Dhaka), plus scores and fixtures for many sports and push-style notifications.

## Build
1. Install Android Studio (Koala or newer), choose **Open**, pick this folder, let Gradle sync.
2. Plug in a phone (USB debugging on) or start an emulator, press **Run**.
   Or from a terminal: `./gradlew assembleDebug` -> `app/build/outputs/apk/debug/app-debug.apk`.
   No Android Studio? Push this folder to GitHub; `.github/workflows/build.yml` builds the APK for you.

## What changed from the Windows version
- Removed: floating widget overlay, taskbar widget, always-on-top, click-through, drag/lock, tray menu, start-with-Windows, font upload, map picker.
- Kept: clock/date/seconds, 12/24h, time zone, weather (Open-Meteo, city search), F1 schedule logic (formula1.com first,
  Jolpica fallback, re-checks time changes), per-session toggles, AMOLED black with the red accent.
- Added: bottom-tab app (Home, Sports, Settings), notifications, sports.

## Notifications
- F1: reminder before each enabled session (at start, 5, 15, 30, 60 min before).
- Followed teams: kick-off reminder, and a "Full time" score when the match ends.
- Scheduled on the phone with exact alarms and a 30-minute background refresh (WorkManager), re-armed after reboot.
  Android 12+ may ask you to allow exact alarms; the Settings tab has a button.
- These are local notifications, not server push (FCM). They work without an account or server, but a result can arrive
  up to about 30 minutes after full time.

## Sports
ESPN public scoreboard feed, no API key: Premier League, La Liga, Bundesliga, Serie A, Ligue 1, Champions League,
Europa League, MLS, NBA, WNBA, NFL, MLB, NHL, UFC, ATP, WTA, PGA Tour, NASCAR, IndyCar. Add a league with one line in
`Models.kt` (`Leagues.all`). Tap a team name to follow it.

## Files
`F1Repo.kt` schedule port · `SportsRepo.kt` scores · `Notifier.kt` alerts and alarms · `Workers.kt` background refresh ·
`AppVm.kt` state · `HomeScreen.kt`, `SportsScreen.kt`, `SettingsScreen.kt` UI.
