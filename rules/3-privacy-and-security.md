# 3. Privacy, Deception, and Device Abuse

Google Play evaluates how apps handle user data, request permissions, and act securely on the device. **Violations here often result in an app suspension (not just a rejection).**

## 3.1 User Data & Prominent Disclosure

Apps that handle sensitive user data (PII, location, contacts, microphones, health info) must explicitly outline usage.

### Prominent Disclosure Requirements:
1. Must be shown **IN-APP** before data collection.
2. Must explain *what* data is collected and *why*.
3. Must require user consent (e.g., "Agree", "I Understand").
4. Cannot only reside in a Privacy Policy link.
5. Cannot be bundled with the system permission dialog.

### Code / UI Implementation

**React Native (Location Flow):**
```javascript
// MUST show a custom modal first
const requestLocation = async () => {
  Alert.alert(
    "Location Permission Needed",
    "This app collects location data to show you nearby friends even when the app is closed. Do you agree?",
    [
      { text: "Disagree", style: "cancel" },
      { text: "Agree", onPress: () => {
         // Now request the SYSTEM permission
         request(PERMISSIONS.ANDROID.ACCESS_BACKGROUND_LOCATION)
      }}
    ]
  );
}
```

## 3.2 Data Safety Section

The Data Safety section in the Play Console must match the app's actual network behavior.
- If you use Firebase/Google Analytics, you MUST declare that your app collects device/installation IDs.
- If you use Sentry/Crashlytics, you MUST declare crash data collection.

## 3.3 Permissions and APIs that Access Sensitive Information

Do not request permissions that are not strictly necessary for the core functionality of the app.

### High-Risk Permissions:
- `READ_SMS`, `RECEIVE_SMS`, `SEND_SMS`
- `READ_CALL_LOG`, `WRITE_CALL_LOG`

**Unless your app is the default SMS or Phone handler, these permissions will lead to rejection.**

### Background Location (`ACCESS_BACKGROUND_LOCATION`)
To use background location, you must submit a video to Google Play showing exactly how the user triggers it and why it's necessary.

### Photo and Video Permissions (2025 Update)
As of 2025, apps are highly restricted from requesting `READ_MEDIA_IMAGES` and `READ_MEDIA_VIDEO`. You must only request these if it is directly tied to the core functionality of the app. Otherwise, use the standard system photo picker (Storage Access Framework).

## 3.4 Malware and Deceptive Behavior (Riskware)

Any app exhibiting malicious behavior will be terminated.
- **Dynamic Code Loading**: Google expressly forbids downloading executable code (.dex, .jar, .so) from third-party servers. All code must be in the APK/AAB or delivered via Play Feature Delivery.
- **Riskware (formerly Maskware)**: Apps that use exploitation techniques to bypass device security or obfuscate malware (Riskware) will be immediately terminated.

**Kotlin Example (Dynamic Code - SUSPENSION RISK):**
```kotlin
// 🔴 DO NOT DO THIS
val classLoader = PathClassLoader("https://my-server.com/malicious.jar", null, parent)
```

**React Native Example (OTA Updates):**
```javascript
// 🟢 CodePush / Expo Updates ARE allowed, provided they do not fundamentally change the app's purpose.
import * as Updates from 'expo-updates'; 
```
But updates cannot add a gambling feature to a calculator app.

## 3.5 Device and Network Abuse

Apps must not interfere with the device, other apps, or network services.
- **Background Processes**: Do not run hidden processes that drain battery or mine cryptocurrency.
- **Notification Abuse**: Do not use system notifications to display ads or promotions unrelated to the app. Notifications must only relate to the app's core feature.
