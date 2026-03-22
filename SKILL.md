---
name: play-store-review
description: Evaluates code against Google Play Developer Program Policies. Use this skill when reviewing Kotlin, Java, Flutter, React Native, or Expo Android app code to identify potential Google Play Store rejection or suspension issues before submission.
license: MIT
metadata:
  author: enes-1
  version: "1.0.0"
---

# Google Play Developer Policy Checker

Comprehensive guide for evaluating Android app code against the Google Play Developer Program Policies. This skill covers EVERY major policy point to identify potential rejection, removal, or suspension issues before submission.

**Supports:** Kotlin, Java, Flutter, React Native, and Expo apps

## When to Apply

Use this skill when:
- Preparing an app for Google Play submission or updates
- Reviewing code for compliance issues (e.g., Target API level updates, Billing Library integration)
- Implementing features that may trigger policy concerns (Permissions, Background Location)
- Auditing existing apps for guideline violations
- Building features involving payments, user data, subscriptions, or sensitive content

## Guideline Sections

Read individual rule files for detailed explanations, checklists, and code examples:

| Section | File | Key Topics |
|---------|------|------------|
| **1. Restricted Content** | [rules/1-restricted-content.md](rules/1-restricted-content.md) | Inappropriate content, UGC, Kids, financial services, gambling |
| **2. Impersonation & IP** | [rules/2-impersonation-and-ip.md](rules/2-impersonation-and-ip.md) | Copyright, trademark, impersonation |
| **3. Privacy & Security** | [rules/3-privacy-and-security.md](rules/3-privacy-and-security.md) | User data, permissions (SMS/Call Log), Data Safety, malware |
| **4. Monetization & Ads** | [rules/4-monetization-and-ads.md](rules/4-monetization-and-ads.md) | Google Play Billing, subscriptions, disruptive ads, ad networks |
| **5. Store Listing** | [rules/5-store-listing-and-promotion.md](rules/5-store-listing-and-promotion.md) | Metadata, deceptive reviews, incentivized downloads |
| **6. Spam & Feature** | [rules/6-spam-and-minimum-functionality.md](rules/6-spam-and-minimum-functionality.md) | Broken features (ANR/Crashes), webview apps, repetitive apps |
| **7. Tech Requirements** | [rules/7-app-quality-and-vitals.md](rules/7-app-quality-and-vitals.md) | Target API, App Bundles, Android Vitals, 64-bit |

## Risk Levels by Category

| Risk Level | Category | Section | Common Rejection/Suspension Reasons |
|------------|----------|---------|--------------------------------------|
| CRITICAL (Suspension) | Privacy & Security | 3.x | Malware, Dynamic code loading, Device abuse, Extreme User Data violations |
| CRITICAL (Suspension) | Payments | 4.1 | Bypassing Google Play Billing for digital goods |
| HIGH (Rejection/Removal) | Privacy & Security | 3.x | Unjustified Sensitive Permissions (`READ_SMS`), Missing Prominent Disclosure |
| HIGH (Rejection/Removal) | Restricted Content | 1.x | Inadequate UGC moderation, violating Families policy |
| MEDIUM (Rejection) | Store Listing / Spam | 5.x / 6.x | Keyword stuffing, Broken features (Crashes, ANRs), Repetitive content |

---

## Quick Reference: High-Risk Rejection Patterns

### Critical Issues (Suspension Risk)

**Kotlin/Java:**
```kotlin
// 🔴 Dynamic code execution from unverified source
val dexClassLoader = DexClassLoader("http://example.com/malicious.dex", ...) // SUSPENSION

// 🔴 Hardcoded secrets or cryptographic keys
val apiKey = "AIzaSy..."

// 🔴 External payment for digital goods
fun purchaseDigitalContent() {
    openStripeCheckout() // Must use Google Play Billing Library
}
```

**React Native / Expo:**
```typescript
// 🔴 Hardcoded secrets in JS bundle
const API_KEY = 'AIzaSy...';

// 🔴 External payment for digital goods
Linking.openURL('https://stripe.com/checkout'); // Use react-native-iap or RevenueCat

// 🔴 Dynamic JS execution downloading from third-party server
eval(downloadedJSCode); // SUSPENSION risk
```

### High-Risk Issues (Rejection)

**Kotlin/Java:**
```kotlin
// 🟡 Requesting Background Location without justification
requestPermissions(arrayOf(Manifest.permission.ACCESS_BACKGROUND_LOCATION), 1)
// Requires a video demonstration and rigorous App Content declaration in Play Console

// 🟡 Missing in-app Subscriptions cancellation link
// Apps that offer subscriptions MUST provide an easy way to cancel them in-app
```

**React Native / Expo:**
```javascript
// 🟡 Collecting precise location without prominent disclosure
navigator.geolocation.getCurrentPosition(...) // If not obvious to user, needs explicit in-app disclosure BEFORE system dialog

// 🟡 Using dangerous permissions unnecessarily
// android.permission.READ_CALL_LOG inside AndroidManifest.xml unless it's a default dialer app
```

### Medium-Risk Issues

```xml
<!-- 🟠 Vague or keyword-stuffed app descriptions -->
<string name="app_desc">Best free poker casino slots poker texas holdem...</string> // REJECTION

<!-- 🟠 Webview-only app without native functionality -->
<WebView android:id="@+id/webview" android:layout_width="match_parent" android:layout_height="match_parent" />
```

---

## Pre-Submission Checklist

### Privacy & Security (Section 3)
- [ ] Valid Privacy Policy link in Play Console and inside the app
- [ ] Prominent in-app disclosure for sensitive data collection
- [ ] Data Safety form correctly filled out outlining data collected and shared
- [ ] No unnecessary permissions declared in `AndroidManifest.xml`
- [ ] No `READ_SMS`, `RECEIVE_SMS`, `READ_CALL_LOG` unless core functionality (Default handler)
- [ ] Targeting the latest required Android API level

### Payments & Monetization (Section 4)
- [ ] Google Play Billing Library used for all digital purchases
- [ ] Subscriptions can be canceled easily via a deep link to Google Play subscription center
- [ ] No disruptive ads (e.g., ads outside the app environment, impossible to dismiss)
- [ ] Ad network complies with Families Policy (if app targets children)

### Restricted Content & Safety (Section 1)
- [ ] No objectionable content (hate speech, sexual content, violence)
- [ ] UGC moderation implemented (filter, report, block, contact)
- [ ] Proper age rating questionnaire completed
- [ ] Kids Category apps comply with strict Families policy (no location collection, proper ads)

### Performance & Spam (Section 6)
- [ ] No crashes or ANRs upon startup
- [ ] App provides a minimum level of functionality (not just a basic web proxy or empty app)
- [ ] All features complete and functional
- [ ] Not a direct clone of another popular app

### Store Listing (Section 5)
- [ ] Title <= 30 chars, no "Free", "No Ads", "Top" keywords
- [ ] Short description <= 80 chars
- [ ] Icon does not contain misleading badges (e.g., fake notification dots, "Sale" badges)
- [ ] Screenshots showcase actual app functionality

### App Quality & Vitals (Section 7)
- [ ] App targets the latest required Android API level in `build.gradle` / project config
- [ ] Published as an Android App Bundle (.aab) with 64-bit support
- [ ] No major ANR risks (e.g., synchronous UI thread blocking)
- [ ] Used SDKs are up to date and not on the vulnerable libraries list
