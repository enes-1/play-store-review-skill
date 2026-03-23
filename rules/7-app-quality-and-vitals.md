# 7. App Quality, Technical Requirements & Android Vitals

Google Play strictly dictates the technical specifications, performance metrics, and modern architectural requirements for all listed apps. Ensuring your app meets these standards helps avoid visibility limits, install warnings, and update rejections.

## 7.1 Target API Level Requirements

Every year, Google Play updates its target API level requirement to ensure apps take advantage of the latest Android security and performance enhancements.
- **New Apps**: Must target an Android API level within one year of the most recent major Android version release (e.g., target API level 35/Android 15 by August 31, 2025).
- **App Updates**: Must also update their target API level within this window to push an update.
- **Play Billing Library**: As of August 2025, all new apps and updates MUST use Play Billing Library version 7 or newer.
- **Consequence**: Apps failing to update their target API will be hidden from new users on newer Android versions.

**Checklist:**
- [ ] Ensure `targetSdkVersion` in `build.gradle` / `app.json` / `AndroidManifest.xml` points to the latest required API (e.g., API 34+ for Android 14).

## 7.2 Application Architecture (App Bundles & 64-bit)

- **Android App Bundles (.aab)**: New apps must publish using the `.aab` format, standardizing device-specific delivery. APKs are no longer accepted for new apps.
- **64-bit Support**: All apps containing native code (e.g., C/C++ libraries via NDK) must provide 64-bit versions (`arm64-v8a`, `x86_64`) alongside any 32-bit versions.

## 7.3 Android Vitals (Performance & Stability)

Google Play measures technical performance heavily. Apps breaching the "bad behavior" thresholds on Android Vitals will lose store visibility or risk removal.
- **Crash Rate**: User-perceived crash rate > ~1.09% is heavily penalized.
- **ANR (Application Not Responding) Rate**: > ~0.47% is heavily penalized.
- **Excessive Wakeups / Battery Drain**: Keep background tasks efficient using WorkManager instead of using Foreground Services indefinitely without user value.

### Code Patterns to Avoid (ANR Risks)

**Kotlin / Java:**
```kotlin
// 🔴 DO NOT run heavy processing on the Main/UI Thread
fun onCreate() {
    val bitmap = BitmapFactory.decodeFile(massiveImageFile) // High Risk of ANR
    val data = networkClient.fetchDataSync() // Never do network calls on Main Thread
}

// 🟢 Use Coroutines or Executors for heavy work
lifecycleScope.launch(Dispatchers.IO) {
    val bitmap = BitmapFactory.decodeFile(massiveImageFile)
}
```

**React Native / Expo:**
```javascript
// 🔴 Synchronous high-cost loops block the JS thread, slowing the native bridge
for (let i = 0; i < 1000000; i++) {
   processData(i);
}

// 🟢 Yield to the event loop, use runOnJS (Reanimated), or use native multi-threading
```

## 7.4 Broken Links and Deprecated SDKs

- **Broken Backend URLs**: If a reviewer cannot load your privacy policy URL, or your app's main API endpoint is dead during review, the app will be rejected.
- **Outdated / Vulnerable 3rd-Party SDKs**: Google Play scans compiled code for known vulnerable SDK versions (e.g., old Billing Libraries, outdated Facebook SDKs). Ensure underlying libraries are frequently updated to avoid automated rejections.
