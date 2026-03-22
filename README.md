# Play Store Review Guidelines Checker

An AI agent skill that exhaustively evaluates Kotlin, Java, Flutter, **React Native**, and **Expo** apps against **every point** in Google Play's Developer Program Policies.

**Supports:** Kotlin, Java, Flutter, React Native, and Expo apps

## Installation

### Claude Code Plugin Marketplace

```bash
/plugin marketplace add enes-1/play-store-review-skill
/plugin install play-store-review@play-store-review
```

### skills.sh

```bash
npx skills add enes-1/play-store-review-skill
```

## Setup

### Supported AI Agents

This skill works with any AI coding agent that supports the skills.sh standard:

- [Claude Code](https://claude.ai/code)
- [Cursor](https://cursor.sh)
- [Windsurf](https://codeium.com/windsurf)
- And other compatible agents

### How It Works

1. **Install the skill** in your project using the command above
2. **Start your AI agent** in the project directory
3. **Ask for a Play Store review** - the agent will automatically load relevant guidelines
4. **Review the findings** - the agent identifies potential rejection issues with code references

### Example Prompts

```
"Review this app for Google Play compliance"
"Check if my Android billing implementation follows Play guidelines"
"Audit the privacy and data collection in this React Native Android app"
"What Play Store issues might block my submission?"
```

## Structure

```
play-store-review-skill/
├── SKILL.md                                 # Index with quick reference & checklist
├── KULLANIM_KILAVUZU.md                     # Detailed Turkish User Manual
└── rules/
    ├── 1-restricted-content.md              # Restricted Content
    ├── 2-impersonation-and-ip.md            # Impersonation & IP
    ├── 3-privacy-and-security.md            # Privacy, Deception, Device Abuse
    ├── 4-monetization-and-ads.md            # Monetization & Ads
    ├── 5-store-listing-and-promotion.md     # Store Listing & Promotion
    └── 6-spam-and-minimum-functionality.md  # Spam & Functionality
```

## Coverage

This skill covers **ALL 6 major policy sections**:

### [1. Restricted Content](rules/1-restricted-content.md)
- Child Endangerment
- Inappropriate Content (Sexual, Hate speech, Violence, Dangerous Organizations)
- Financial Services, Real-Money Gambling
- Illegal Activities, Marijuana, Tobacco, Alcohol

### [2. Impersonation & IP](rules/2-impersonation-and-ip.md)
- Impersonation of other apps/entities
- Copyright Infringement
- Trademark Infringement
- Counterfeit Goods

### [3. Privacy & Security](rules/3-privacy-and-security.md)
- User Data & Data Safety
- Permissions & APIs that Access Sensitive Information (SMS/Call Log)
- Device and Network Abuse (Background location, dynamic code loading)
- Malware & Mobile Unwanted Software

### [4. Monetization & Ads](rules/4-monetization-and-ads.md)
- Google Play Billing
- Subscriptions (management, cancellation)
- Ads, Disruptive Ads
- Families Policy Ad Requirements

### [5. Store Listing](rules/5-store-listing-and-promotion.md)
- Metadata (misleading titles, descriptions, icons)
- User Ratings & Reviews
- Incentivized Ratings

### [6. Spam & Functionality](rules/6-spam-and-minimum-functionality.md)
- Minimum Functionality
- Repetitive Content (White-label apps)
- Webviews and Affiliate Spam
- Broken Functionality and ANRs/Crashes Threshold

### [7. App Quality & Vitals](rules/7-app-quality-and-vitals.md)
- Target API Level Requirements
- App Architecture (AAB, 64-bit)
- Android Vitals (Crash Rate, ANR Rate)
- Broken Links and Deprecated/Vulnerable SDKs

## License

MIT
