# Ability Board (Android app)

Offline grade and GPA tracker on the Northrise scale. The web app lives in `www/index.html`;
Capacitor wraps it as an Android APK. All data stays on the phone. No server, no internet needed.

## Get the APK (no Android Studio needed)
1. Create an empty GitHub repo and push this folder to it:
   ```
   git init
   git add .
   git commit -m "Ability Board Android app"
   git branch -M main
   git remote add origin https://github.com/<your-username>/ability-board-app.git
   git push -u origin main
   ```
2. On GitHub open the **Actions** tab, then **Build Android APK**. It starts by itself after the push
   (or press **Run workflow**). It takes about 5 to 8 minutes.
3. Open the finished run, scroll to **Artifacts**, download **ability-board-apk**, unzip it.
4. Copy `app-debug.apk` to your phone and open it. Android will ask you to allow
   "Install unknown apps" for your file manager or browser. Allow it for that one install.

## Updating the app later
Edit `www/index.html`, commit and push. Download the new APK and install it over the old one.
Your data is kept, because every build is signed with the same key in `keystore/debug.keystore`.
Back up first anyway: Setup, Data, **Save backup file**.

## Before you uninstall or change phones
Uninstalling deletes the data. Use **Save backup file**, keep the file in Drive, then on the
new install use **Load backup file** and **Import data**.

## Build locally instead (optional)
Needs Node 22+, JDK 21 and Android Studio.
```
npm ci
npx cap add android
npx cap sync android
npx cap open android
```
After editing `www/`, run `npx cap sync android` again.

## Notes
- This is a debug-signed APK for your own phone. For the Play Store you would need a proper
  release keystore (keep it private and never commit it).
- `keystore/debug.keystore` is only a sideloading key with the standard password `android`.
  It is not a secret, so do not reuse it for anything else.
- Images and animated backgrounds are stored on the device and are not part of backup files.
