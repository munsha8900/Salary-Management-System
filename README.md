# Coffer — Android (APK)

Coffer is an offline employee money-management app: employees, salary structure,
payroll with payslips, advances & loans, project-based payment, per-employee
ledger, and reports. This project wraps the app in a native Android WebView.

The app is **fully self-contained**: React, the fonts, and the compiled app code
are bundled in `app/src/main/assets/`. There is **no `INTERNET` permission** and
no network calls. Data persists on-device via the WebView's localStorage.

## Get the APK — Option A: GitHub Actions (no tools to install)

1. Create a new GitHub repository.
2. Push this folder to it (the `coffer-android` contents at the repo root):
   ```bash
   cd coffer-android
   git init && git add . && git commit -m "Coffer Android"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
3. Open the repo's **Actions** tab. The **Build Coffer APK** workflow runs
   automatically on push (or run it manually with **Run workflow**).
4. When it finishes, open the run and download the **coffer-debug-apk** artifact.
   Inside is `app-debug.apk`.
5. Copy it to your phone and install (enable "install from unknown sources").

## Get the APK — Option B: Android Studio

1. Open this folder in Android Studio (Giraffe or newer).
2. Let it sync. **Build > Build App Bundle(s) / APK(s) > Build APK(s)**.
3. The APK lands in `app/build/outputs/apk/debug/app-debug.apk`.

## Get the APK — Option C: command line

Requires JDK 17 + Android SDK (set `ANDROID_HOME` / `sdk.dir` in `local.properties`).
```bash
gradle assembleDebug      # or ./gradlew assembleDebug if you add the wrapper
```

## Notes

- This produces a **debug-signed** APK, which installs directly on any device —
  ideal for internal use. For a Play Store / release build you'll add a signing
  keystore and a `release` signing config.
- App id: `com.markfold.coffer` · version 1.0 · minSdk 24 (Android 7.0+).
- To change the name shown on the home screen, edit `res/values/strings.xml`.
- To update the app itself, replace `app/src/main/assets/index.html` /
  `app.js` and rebuild.
