# 1. Restricted Content

Google Play policies are strict regarding the type of content distributed on the platform. Apps containing or promoting inappropriate, illegal, or restricted content will be rejected or suspended.

## 1.1 Inappropriate Content

Google strictly prohibits apps that contain or promote:

- **Sexual Content**: Apps depicting sexual acts, pornography, or overly graphic content.
- **Hate Speech**: Content inciting violence, discrimination, or hatred against protected groups.
- **Violence**: Gratuitous violence, blood, gore, or animal cruelty.
- **Self-Harm**: Content promoting suicide, eating disorders, or self-injury.
- **Dangerous Organizations**: Content related to terrorism or criminal groups.

### Checklist
- [ ] Remove all overly explicit sexual or violent imagery.
- [ ] Ensure language is free from hate speech.

## 1.2 User-Generated Content (UGC)

Apps containing UGC (forums, social networks, matching platforms) must have robust moderation.

### Requirements for UGC:
- **Terms of Use**: Users must agree to UGC terms.
- **Moderation**: Implement a system to filter/moderate objectionable content.
- **Reporting**: Users must be able to report abusive users and content.
- **Blocking**: Users must be able to block abusive users.
- **Action**: Developer must take action against reported content within 24 hours.

### Code / UI Implementation

**React Native Example (Reporting System):**
```javascript
// MUST BE PRESENT in UGC apps
const handleReportUser = async (userId, reason) => {
    await api.post('/report', { targetId: userId, reason });
    Alert.alert("Reported", "Thank you, our moderation team will review within 24 hours.");
}

const handleBlockUser = async (userId) => {
    // Implement block logic immediately in UI
}
```

## 1.3 Financial Services

Apps that manage or engage in financial services (banking, loans, crypto) must comply with local regulations.
- **Personal Loans**: Must disclose APR, repayment periods (cannot be <= 60 days), and full cost.
- **Cryptocurrency**: Cannot mine cryptocurrency on the device. Can manage remote mining.

## 1.4 Real-Money Gambling

Only permitted in specific jurisdictions and apps must be classified as "Adult" and have an official gambling license from the target country.
- Must prevent usage from restricted regions (Geo-blocking).

## 1.5 Families Policy & Kids Category

If your app targets children:
- Must NOT collect precise location or device IDs (IMEI, MAC).
- Ads must only come from Google Play Certified Ad Networks targeting children.
- Neutral age screens must be used for age gating.
