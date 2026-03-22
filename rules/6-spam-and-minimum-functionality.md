# 6. Spam and Minimum Functionality

Google Play ensures that apps provide a baseline level of functionality and a respectful user experience. Apps that are broken, repetitive, or exist solely to drive traffic to a website will be rejected.

## 6.1 Minimum Functionality

Apps must not crash, force close, freeze, or otherwise function abnormally.

### Crash & ANR Requirements
- Google Play strictly monitors the **Application Not Responding (ANR)** and **Crash** rates in Android Vitals.
- Apps with high crash rates (> 1.09% user-perceived crash rate) will have their visibility reduced in the Play Store and may be suspended.

### Barren Applications
Apps must provide some degree of user utility.
- An app cannot be just a basic proxy to a website (WebView-only app).
- Apps must utilize native Android features, offline capabilities, or provide enhanced experiences over the mobile web version.

**React Native WebView-only App (High Rejection Risk):**
```javascript
// 🟠 Providing only a WebView pointing to a website with no native features
const App = () => {
  return <WebView source={{ uri: 'https://m.mywebsite.com' }} />;
};
```
*Fix: Add native push notifications, bottom tabs, an offline state, or native sharing.*

## 6.2 Repetitive Content (Spam)

Publishing multiple apps that have highly similar functionality, content, and user experience is considered spam.
- **White-Label Apps**: If you create similar apps for different clients (e.g., 50 different church apps or 100 different restaurant menus), you should combine them into one unified app where users select their specific branch or client.

## 6.3 Affiliates and Web Spam

Apps whose primary purpose is to drive affiliate traffic to a website or provide a web experience without permission from the website owner are not allowed.
- You cannot create an app that just loads `amazon.com` or `wikipedia.org` inside a webview and injects your own ads or affiliate links.

## 6.4 Broken Features

All features advertised must work.
- If you have an "Export to PDF" button, it must successfully generate a PDF.
- If an app requires login credentials, you must provide a functional **Demo Account** in the App Content section of the Google Play Console for reviewers to test.
