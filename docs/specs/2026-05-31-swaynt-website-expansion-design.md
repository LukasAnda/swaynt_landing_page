# Swaynt Website Expansion — Design Spec

## Overview

Expand the Swaynt landing page from a single-page site to a multi-page website to meet Apple Developer Program enrollment requirements. Apple requires company websites to have substantial content — not "minimal content" placeholder pages.

**Company:** Swaynt LLC  
**Founded:** 2026  
**Location:** 75 E 3rd St, Sheridan, WY 82801, USA  
**Contact:** support@swaynt.com  
**Focus:** Mobile app development using Kotlin Multiplatform (KMP)

## Site Structure

```
index.html      → Home (updated)
about.html      → About / Company
services.html   → Services (mobile/KMP focus)
contact.html    → Contact
privacy.html    → Privacy Policy
```

## Navigation

Consistent header across all pages:

```
[SWAYNT]                    About   Services   Contact
```

- Logo links to home
- Current page gets subtle visual indicator (white text vs muted)
- Privacy Policy linked in footer only (standard practice)

## Footer

Consistent footer across all pages:

```
────────────────────────────────────────────────────────
© 2026 Swaynt LLC                         Privacy Policy
75 E 3rd St, Sheridan, WY 82801           support@swaynt.com
```

## Page Designs

### Home (index.html)

**Changes from current:**
- Update navigation: add About, Services, Contact links
- Update services grid: mobile-focused instead of 4 generic services
- Update footer: add address, privacy link, proper legal line

**Hero section:** Keep as-is — "We build digital products that matter."

**Services grid (updated):**

| # | Title | Description |
|---|-------|-------------|
| 01 | iOS & Android | Native apps for both platforms |
| 02 | Kotlin Multiplatform | One codebase, native performance on both |
| 03 | Quality First | Clean code, tested, built to last |
| 04 | Full Lifecycle | From concept to App Store submission |

### About (about.html)

**Layout:** Simple prose-based design, no separate stats/columns.

**Content structure:**
1. Headline: "Building software with intention."
2. Intro paragraph: Swaynt is an independent software studio founded in 2026. We craft mobile apps and games with a focus on quality over quantity.
3. Philosophy paragraph: We believe great software comes from small teams with clear vision. Every project gets our full attention — no assembly lines, no shortcuts.

**Tone:** Confident indie studio positioning. Honest about being small, framing it as intentional focus rather than limitation.

### Services (services.html)

**Focus:** Mobile app development with Kotlin Multiplatform

**Content structure:**
1. Headline: "Mobile Apps" or "Mobile Development"
2. Intro: What we build and why mobile is our focus
3. KMP explanation: What Kotlin Multiplatform is, benefits (shared logic, native UI, faster development, native performance)
4. Our approach: How we work, what clients can expect
5. Platforms: iOS and Android from a single codebase

**Subsections to cover:**
- Why KMP (benefits over pure native or cross-platform alternatives)
- Development process
- What you get (deliverables)

### Contact (contact.html)

**Layout:** Simple, clean — just contact information.

**Content:**
```
Get in touch
────────────────────────────────────

Email
support@swaynt.com

Address
75 E 3rd St
Sheridan, WY 82801
USA
```

**No contact form** — direct email only.

### Privacy Policy (privacy.html)

**Scope:** Covers both swaynt.com website and mobile apps/games published by Swaynt.

**Sections:**

1. **Introduction**
   - Who we are (Swaynt LLC)
   - What this policy covers (website and mobile applications)

2. **Information We Collect**
   - Website: basic analytics (if applicable), cookies
   - Apps: device information, usage analytics, advertising identifiers

3. **How We Use Your Information**
   - Improve app performance and user experience
   - Display relevant advertisements
   - Fix bugs and crashes
   - Analyze usage patterns

4. **Third-Party Services**
   - Advertising networks (e.g., Google AdMob)
   - Analytics providers (e.g., Firebase Analytics)
   - Note that these services have their own privacy policies

5. **Data Retention**
   - How long data is kept
   - Anonymization practices

6. **Your Rights**
   - Right to access, correct, or delete data
   - How to contact us with requests

7. **Children's Privacy**
   - COPPA compliance
   - Age restrictions if applicable
   - Parental consent requirements

8. **Changes to This Policy**
   - How updates are communicated
   - Effective date tracking

9. **Contact Us**
   - support@swaynt.com for privacy-related questions

**Tone:** Clear and readable, not dense legalese. Follows standard privacy policy conventions while being accessible.

## Visual Design

**Maintain existing aesthetic:**
- Dark theme (--bg: #080808)
- Typography: DM Serif Display (headings) + Outfit (body)
- Subtle animations on page load
- Grain texture overlay
- Color palette: white text, muted grays for secondary text, subtle borders

**Responsive:** All pages must work on mobile, tablet, and desktop (matching current breakpoints).

## Technical Notes

- Static HTML/CSS site (GitHub Pages compatible)
- No build process required
- Email obfuscation for spam protection (current pattern can be reused)
- All pages share consistent CSS (can be extracted to shared stylesheet or kept inline)

## Success Criteria

1. Apple Developer Program enrollment passes website review
2. All 5 pages are live and accessible
3. Navigation works between all pages
4. Mobile responsive on all pages
5. Privacy policy covers website + apps with ads/analytics
6. Footer with legal info appears on all pages
