# Mini Farm 3D Legend - Capacitor Android project

## Open in Android Studio
1. Unzip, then in this folder run:  npm install
2. npm run sync        (builds Tailwind CSS + copies www/ into android/)
3. npm run open        (or: Android Studio > Open > select the `android` folder)
4. Let Gradle sync finish, then Build > Build APK(s)
   Output: android/app/build/outputs/apk/debug/app-debug.apk

## After editing www/index.html
Run `npm run sync` again, then rebuild in Android Studio.
(Tailwind is compiled locally from www/index.html, so new classes need the sync step.)

## Notes
- Offline-ready: three.js (r128) is in www/vendor, Tailwind CSS is prebuilt in www/css.
- Only change vs. original HTML: the two CDN <script> tags (lines 11-12) now point to local files.
- Save data uses localStorage (cloud save only runs if a Firebase config is injected, which it isn't here).
- App ID: com.marcjoseph.minifarm3d  (change in capacitor.config.json before first `cap add`, or edit applicationId in android/app/build.gradle + package folder).
"# Mini-Farm-Legend" 
