# 5. Store Listing and Promotion

Google Play requires that your Store Listing correctly reflects your app. Misleading claims or attempts to manipulate ratings are strictly forbidden.

## 5.1 Misleading Metadata

Your app's Title, Short Description, and Long Description must be accurate and free of keyword stuffing or deceptive language.

### Formatting Rules:
- **App Title**: Max 30 characters.
- **Short Description**: Max 80 characters.
- **No Promotional Keywords in Title/Icon**: You cannot use words like "Free", "Sale", "Top", "Best", "Update", "No Ads" in the title or icon.

**Bad Title Example:** `Best Poker Calculator Free No Ads` (REJECTION)
**Good Title Example:** `Poker Odds Calculator`

### Icon Rules:
- Do not add graphic elements that indicate ranking (e.g., "#1 App").
- Do not add fake notification dots (e.g., a red circle with a "1" to look like an unread message).

## 5.2 Screenshots and Video

Screenshots and videos must show the actual in-app experience.
- Do not use images of people holding a phone if the app screen is too small to see.
- Show core gameplay or app functionality.

## 5.3 Incentivized Ratings, Reviews, and Installs

Developers must not manipulate their app's placement on Google Play.

- **Fake Reviews**: Do not pay users or offer rewards in exchange for a 5-star review.
- **Requiring Ratings**: You cannot force a user to rate the app to unlock a feature.
- **Conditional Ratings**: Do not say "Rate us 5 stars to get 100 coins!"

**React Native Violation:**
```javascript
// 🔴 Bribing users for a rating
const unlockLevel = () => {
    Alert.alert("Unlock Level 2", "Give us a 5-star review on Google Play to unlock this level!", [
        { text: "Rate Now", onPress: openPlayStore }
    ]);
};
```

### Best Practice for Ratings
Use the official In-App Review API, which does not allow custom text prompting for a specific rating score.

**React Native (react-native-in-app-review):**
```javascript
import InAppReview from 'react-native-in-app-review';

// 🟢 Correct Usage
const promptReview = () => {
  if (InAppReview.isAvailable()) {
    InAppReview.RequestInAppReview();
  }
}
```
