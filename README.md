# Food-n-Me — App Setup Guide

This folder is a ready-to-go Capacitor project. Your app's actual content
(HTML/CSS/JS) lives in `www/index.html` — it's the same Food-n-Me planner,
just wrapped so it can run as a native iOS/Android app.

## Prerequisites

- **Node.js** (v18+) — https://nodejs.org
- **For iOS:** a Mac with **Xcode** installed (free from the Mac App Store)
  and an Apple Developer account ($99/year) to publish
- **For Android:** **Android Studio** installed
  and a Google Play Developer account ($25 one-time) to publish

## 1. Install dependencies

From inside this folder:

```bash
npm install
npx cap init
```

(`cap init` will ask for app name / package id — you can just press Enter
to accept the values already set in `capacitor.config.json`.)

## 2. Add the native platforms

```bash
npx cap add ios
npx cap add android
```

This generates `ios/` and `android/` folders containing full native Xcode
and Android Studio projects.

## 3. Sync your web app into the native projects

Run this any time you change files in `www/`:

```bash
npx cap sync
```

## 4. Open and run

```bash
npx cap open ios       # opens Xcode
npx cap open android   # opens Android Studio
```

From Xcode or Android Studio, pick a simulator/emulator or a connected
device and hit Run (▶) to test the app.

## 5. App icon & splash screen

Capacitor apps need proper icons and splash screens for every device size.
The easiest way is the `@capacitor/assets` generator:

```bash
npm install @capacitor/assets --save-dev
```

Then create two source images in this folder:
- `resources/icon.png` — 1024×1024px, no transparency
- `resources/splash.png` — 2732×2732px, logo centered on background

Then run:

```bash
npx capacitor-assets generate
```

This auto-generates every required icon/splash size for iOS and Android
and drops them into the native projects.

## 6. A note on data storage

The app currently saves meal plans and recipes with `localStorage`, which
works fine inside the Capacitor webview but is **local to each device**
(no sync between phones, and data can be lost if the app is uninstalled).
If you'd like data to sync across devices or survive reinstalls, the next
step would be swapping `localStorage` for `@capacitor/preferences` (still
local, but more robust) or a small backend + account system (for real
cross-device sync).

## 7. Publishing

- **iOS:** Archive the app in Xcode → upload to App Store Connect → submit
  for review.
- **Android:** Build a signed `.aab` in Android Studio → upload to the
  Google Play Console → submit for review.

Both stores will ask for screenshots, a description, privacy policy URL,
and an app icon — worth preparing those ahead of submission.
