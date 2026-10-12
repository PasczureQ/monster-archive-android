# Monster Archive: Endless (Android app)

Pixel-art idle monster game packaged for Android 15 (API 35) with Capacitor 7.
The whole game is one file: `www/index.html`. App id: `com.monsterarchive.endless`. Works fully offline.

## Easiest: get an APK with no installs (GitHub Actions)
1. Create a new GitHub repository and upload everything in this folder (keep the `.github` folder).
2. Open the **Actions** tab, pick **Build Android APK**, press **Run workflow** (it also runs on every push).
3. When it finishes, download the **monster-archive-debug-apk** artifact, unzip it, and copy `app-debug.apk` to your phone.
4. Open the APK on the phone and allow "Install unknown apps" for your file manager or browser when asked.

## Build locally with Android Studio
1. Install Node 20+ and Android Studio (it brings JDK 21 and the SDK).
2. In this folder run `npm install`, then `npx cap sync android`, then `npx cap open android`.
3. Press Run to launch on a phone or emulator, or use Build > Build APK(s).
Command line instead: `cd android && ./gradlew assembleDebug` (APK at `android/app/build/outputs/apk/debug/`).

## Publishing to Google Play
1. Create a keystore: `keytool -genkey -v -keystore release.jks -alias monster -keyalg RSA -keysize 2048 -validity 10000`
2. Add a signing config to `android/app/build.gradle`, then run `cd android && ./gradlew bundleRelease`.
3. Upload `android/app/build/outputs/bundle/release/app-release.aab` in the Play Console. Keep the keystore safe and never commit it.
Raise `versionCode` in `android/app/build.gradle` for every upload.

## Editing the game
Edit `www/index.html`, then run `npx cap sync android` and rebuild.

## Install without an APK (PWA)
Host the `www` folder on any HTTPS site (GitHub Pages works). Open it in Chrome on Android and use Menu > Install app.

## Notes
* Saves live in the app's local storage. Use Settings > Export save to back up or move progress.
* Admin panel: Settings > Admin panel, password `monsteradmin` (single-player cheats only).
* Back button closes menus, returns to Battle, then minimizes the app. Portrait only. Vibration permission is included.
