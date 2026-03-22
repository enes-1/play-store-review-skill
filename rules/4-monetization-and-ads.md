# 4. Monetization and Ads

Google Play sets strict guidelines regarding monetization models, subscriptions, and advertisement placements.

## 4.1 Google Play Billing

Apps offering **digital goods** or services must use Google Play's Billing Library.

**Digital Goods Definition:**
- Virtual currencies, extra lives, ad-free features, premium content, digital subscriptions (e.g., streaming services, gym memberships inside an app).

**Physical Goods/Services (DO NOT use Google Play Billing):**
- Physical retail items (clothes, electronics), food delivery, ride-sharing, financial services (e.g., buying stock). Here, use Stripe, PayPal, or Braintree.

### Example Violations
**React Native / Expo:**
```javascript
// 🔴 External payment for digital goods (e.g., unlocking a feature)
Linking.openURL('https://mywebsite.com/upgrade'); // REJECTION

// 🟢 Using Google Play Billing via RevenueCat or react-native-iap
import Purchases from 'react-native-purchases';
await Purchases.purchasePackage(package);
```

**Kotlin / Java:**
```kotlin
// 🔴 Using Stripe for unlocking an app feature
val intent = Intent(this, StripeActivity::class.java)

// 🟢 Using standard BillingClient
billingClient.launchBillingFlow(activity, billingFlowParams)
```

## 4.2 Subscriptions

If your app sells auto-renewing subscriptions, it must:
- Clearly communicate offer terms (price, duration, free trial length).
- NOT hide the cost or make users scroll to see it.
- **Must provide an easy-to-use cancellation process deeply linked into the app.**

### Deep Link for Cancellation:
You must provide a link to Play Store Subscriptions:
`https://play.google.com/store/account/subscriptions`

```javascript
// React Native Cancellation link
<Button 
  title="Manage Subscriptions" 
  onPress={() => Linking.openURL('https://play.google.com/store/account/subscriptions')} 
/>
```

## 4.3 Disruptive Ads

Ads must not interfere with normal app use.
- **Interstitial Ads**: Cannot suddenly appear during gameplay or when a user is actively engaging with a feature.
- **Dismissal**: All full-screen ads must be closable within a reasonable time (usually 5 seconds).
- **Out-of-App Ads**: Ads must not display outside the app environment (e.g., popping up on the home screen when the app is closed).
- **Lockscreen Ads**: Apps cannot introduce ads or features that monetize the locked display of a device.

## 4.4 Families Policy Ads

If the app targets children (under 13):
- Only use **Google Play Certified Ad Networks**.
- Ads must not be deceptive, have excessive blood, or include inappropriate imagery.
- Ads must have a clear "Ad" label.
