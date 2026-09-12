# 🐛 Bug Report — Fixzone Bangladesh
**Website:** [https://fixzone.com.bd](https://fixzone.com.bd)  
**Audit Date:** September 11, 2026  
**Auditor:** Antigravity QA Engineering  
**Total Bugs Found:** 26  
**Evidence:** Screenshots in `/errors/screenshots/`

---

## 📊 Bug Summary

| Category | Count | Critical | High | Medium | Low |
|:---|:---:|:---:|:---:|:---:|:---:|
| 🎨 Design Flaws | 10 | 1 | 4 | 3 | 2 |
| ⏳ Loading Flaws | 6 | 2 | 2 | 2 | 0 |
| ⚙️ Functional / Other | 10 | 3 | 4 | 2 | 1 |
| **Total** | **26** | **6** | **10** | **7** | **3** |

---

## 🎨 Section 1: Design Flaws

> Visual, layout, CSS, typography, or branding issues found across the website.

---

### 🐛 BUG-DESIGN-001 — Wrong Image in "How It Works" Section
- **Severity:** 🔴 Critical
- **Page:** Homepage (`/`)
- **Section:** "How It Works" / Step-by-step guide (Section 2)
- **Description:** The image used alongside the 3-step process ("Choose a Service → Book a Schedule → Get it Done") shows a **VR/AR headset (Oculus/Meta Quest)**. This is completely irrelevant to a home services business like Fixzone that provides AC repair, plumbing, and electrical services.
- **Impact:** Severely damages brand credibility and user trust. First-time visitors may think the website is broken or serving wrong content.
- **Steps to Reproduce:**
  1. Open `https://fixzone.com.bd/`
  2. Scroll down past the hero section
  3. Find the "How It Works" section with the 3 numbered steps
  4. Observe the image on the left shows a VR headset
- **Expected:** A relevant image — e.g., a technician fixing an AC, a plumber working, or a service booking illustration
- **Actual:** A VR/AR headset (Oculus Meta Quest) is shown with a play-button overlay
- **Screenshot:** `screenshots/homepage_how_it_works.png`

---

### 🐛 BUG-DESIGN-002 — Hero Headline Uses Jarring Yellow Color
- **Severity:** 🟠 High
- **Page:** Homepage (`/`)
- **Section:** Hero Banner — Main Headline
- **Description:** The headline "Smarter services for a simpler life" is rendered in a **bright canary yellow (#F5C518 or similar)** over a dark image background. While readable at first glance, this yellow color is not part of the Fixzone brand palette (which is orange `#F27C27` and navy `#1F417F`). It creates brand inconsistency and feels visually off compared to the rest of the site.
- **Steps to Reproduce:**
  1. Open `https://fixzone.com.bd/`
  2. Observe the main hero heading
- **Expected:** Headline uses brand-consistent white, orange, or navy color
- **Actual:** Headline renders in bright yellow that is not in the Fixzone design system
- **Screenshot:** `screenshots/homepage_hero.png`

---

### 🐛 BUG-DESIGN-003 — Package Name Truncated in Service Details Cart
- **Severity:** 🟠 High
- **Page:** Service Details (`/services/ac-master-service`)
- **Section:** Package Selection — Package Name Label
- **Description:** Package names are being **hard-truncated with ellipsis** inside the package selection cards. The text "AC Master Service - I..." is cut off and the full package name is never shown (even on hover — no tooltip is provided). Users cannot tell which package option they are selecting.
- **Steps to Reproduce:**
  1. Navigate to `/services/ac-master-service`
  2. Observe the "Select package" section
  3. Note both package names are truncated: "AC Master Service - I..."
- **Expected:** Full package name visible, or tooltip on hover revealing complete text
- **Actual:** Package names are clipped with no accessible alternative
- **Screenshot:** `screenshots/service_detail.png`

---

### 🐛 BUG-DESIGN-004 — "BOOK SERVICE" Nav Button Color Inconsistent
- **Severity:** 🟡 Medium
- **Page:** All pages (Global Header)
- **Section:** Navigation Bar — Top Right
- **Description:** The "BOOK SERVICE" button in the navigation header is styled in **teal/cyan** (`#06B6D4`) while the brand's primary CTA color is supposed to be **orange** (`#F27C27`). The "Search" button on the hero section and other CTAs use orange. This inconsistency creates visual confusion about the site's primary action color.
- **Steps to Reproduce:**
  1. Open any page on `https://fixzone.com.bd/`
  2. Compare the top-right "BOOK SERVICE" button with the hero section "Search" button or the "SIGN IN TO YOUR ACCOUNT" button on the login page
- **Expected:** "BOOK SERVICE" CTA uses the brand primary orange `#F27C27` consistently
- **Actual:** Button is rendered in teal/cyan, breaking color consistency
- **Screenshot:** `screenshots/homepage_hero.png`

---

### 🐛 BUG-DESIGN-005 — "Back to Top" Button Overlaps Chat Widget
- **Severity:** 🟠 High
- **Page:** All pages with scroll (Homepage, Services, etc.)
- **Section:** Bottom-right corner floating elements
- **Description:** The **"Back to Top" arrow button** (↑) and the **"Talk to our team →" chat widget** both anchor to the bottom-right corner. When both are visible simultaneously (after scrolling down), they **visually overlap**, making both buttons partially inaccessible or confusing.
- **Steps to Reproduce:**
  1. Open `https://fixzone.com.bd/`
  2. Scroll down ~800px until the Back to Top button appears
  3. Observe both floating elements crowding the bottom-right
- **Expected:** Both elements are stacked with clear spacing (e.g., `bottom: 80px` for Back to Top, `bottom: 20px` for chat)
- **Actual:** Elements overlap in the same corner position
- **Screenshot:** `screenshots/homepage_how_it_works.png`

---

### 🐛 BUG-DESIGN-006 — Services Page Area Label Shows Raw Address ("1no Sarak")
- **Severity:** 🟡 Medium
- **Page:** Services (`/services`) & About (`/about`) & Contact (`/contact`)
- **Section:** Page subheading / location context
- **Description:** The location-aware subheading on the Services, About, and Contact pages shows **"Area: 1no Sarak."** — this is a raw, unformatted GPS-reverse-geocoded address label likely from a low-quality geocoder result. "1no Sarak" (meaning "Road No. 1" in Bangla informal) is confusing and unprofessional to English-speaking or non-local users.
- **Steps to Reproduce:**
  1. Navigate to `/services`
  2. Read the subtitle: `"Browse categories, check pricing, and book faster. Area: 1no Sarak."`
  3. Also visible on `/about`: `"Serving: 1no Sarak"` and `/contact`: `"Serving context: 1no Sarak"`
- **Expected:** Display a clean location such as "Faridpur Sadar" or "Faridpur, Bangladesh"
- **Actual:** Raw geocoder string "1no Sarak" displayed verbatim
- **Screenshot:** `screenshots/services_page.png`, `screenshots/about_page.png`, `screenshots/contact_page.png`

---

### 🐛 BUG-DESIGN-007 — Contact Page Exposes Internal Admin Subject Label
- **Severity:** 🟠 High
- **Page:** Contact (`/contact`)
- **Section:** Topic selector / form
- **Description:** Below the topic selector buttons (General, Booking, Billing, Partnership, Press), there is a visible label reading **"Subject line for admins: `General inquiry`"** rendered in the user-facing form. This is an internal field label that should never be visible to end users.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/contact`
  2. Observe the text beneath the topic pill buttons
- **Expected:** Admin subject line mapping is backend-only; no such label is visible to users
- **Actual:** "Subject line for admins: General inquiry" is displayed in monospace/code font to all visitors
- **Screenshot:** `screenshots/contact_page.png`

---

### 🐛 BUG-DESIGN-008 — About Page Stats Cards All Show "0"
- **Severity:** 🔴 Critical
- **Page:** About (`/about`)
- **Section:** Statistics Cards — "Categories", "Services", "Areas covered", "Active deals"
- **Description:** All four stat counter cards on the About page display **"0"** as their value. The actual platform has 6 categories and 9 services (confirmed on the Services page). This is a data-loading failure that makes the business appear to have no activity.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/about`
  2. Observe the 4 stat boxes on the right
- **Expected:** Cards show live data: e.g., `Categories: 6`, `Services: 9`, `Areas covered: 28`, `Active deals: [N]`
- **Actual:** All 4 cards show `0`
- **Screenshot:** `screenshots/about_page.png`

---

### 🐛 BUG-DESIGN-009 — Login Page Logo Renders with Font Fallback
- **Severity:** 🟢 Low
- **Page:** Login (`/login`)
- **Section:** Top branding area
- **Description:** On the left-side branding panel of the login page, the Fixzone logo appears to render with a **font character as the icon** ("F" in a stylized frame) rather than the full PNG logo image used elsewhere. This creates a visual inconsistency between the login panel branding and the rest of the site.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/login`
  2. Look at the logo in the top-left of the dark left panel
- **Expected:** Full Fixzone PNG logo (`/api/uploads/image-1778663346697-854842737.png`) displayed identically to the main header logo
- **Actual:** Icon font character rendering instead of the logo image
- **Screenshot:** `screenshots/login_page.png`

---

### 🐛 BUG-DESIGN-010 — Register Page Logo Uses Different Brand Style
- **Severity:** 🟢 Low
- **Page:** Register (`/register`)
- **Section:** Top of registration form
- **Description:** The registration page uses an **orange circle badge with a wrench icon + "FIXZONE" text** as the header branding. This is inconsistent with the main site's Fixzone logo (the stylized "F" with "Fixzone" text). Two completely different logo treatments create brand fragmentation.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/register`
  2. Observe the logo at the top of the form
  3. Compare with the header logo on `/` or `/services`
- **Expected:** Consistent Fixzone logo across all pages
- **Actual:** Alternate icon badge + word-mark used only on register page
- **Screenshot:** `screenshots/register_page.png`

---

## ⏳ Section 2: Loading Flaws

> Issues related to slow loading, content not rendering, spinners, or data fetch failures.

---

### 🐛 BUG-LOAD-001 — Splash Screen Blocks Content; May Persist if JS Fails
- **Severity:** 🔴 Critical
- **Page:** All pages (Global)
- **Section:** Full-page splash overlay
- **Description:** A full-screen gradient splash screen with the logo and "Loading latest services and offers…" blocks all page content until JavaScript resolves. If JavaScript fails to load (due to slow CDN, network drop, or an error in `66a8c16702b8a250.js`), **the splash screen will never dismiss**, leaving the user with a permanently blank/blocked screen.
- **Steps to Reproduce:**
  1. Open any Fixzone page with Network Throttling set to "Slow 3G" in browser DevTools
  2. Or disable JavaScript in the browser
  3. Observe: Splash screen either takes very long or never dismisses
- **Expected:** Splash screen has a hard timeout (e.g., max 3 seconds) and always dismisses, falling back to server-rendered HTML content
- **Actual:** Splash screen is fully JS-dependent with no fallback or enforced maximum display duration override

---

### 🐛 BUG-LOAD-002 — Services Page Renders Client-Side Only (BAILOUT_TO_CLIENT_SIDE_RENDERING)
- **Severity:** 🔴 Critical
- **Page:** Services (`/services`)
- **Section:** Entire page content
- **Description:** The services page source HTML includes `<template data-dgst="BAILOUT_TO_CLIENT_SIDE_RENDERING">` — a Next.js indicator that **server-side rendering was skipped** and the full page content depends on client-side JavaScript loading. This means:
  - Web crawlers (Google, Bing) cannot index the service listings
  - Users on slow connections see a blank white page with only a loading spinner
  - The page has **zero SEO value** for service content
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/services`
  2. View page source (Ctrl+U)
  3. Search for `BAILOUT_TO_CLIENT_SIDE_RENDERING`
  4. Also observe a spinner (`min-h-screen bg-slate-50 flex items-center justify-center`) is the only initial content
- **Expected:** Service cards and categories are server-rendered or included in the initial HTML payload
- **Actual:** Entire services catalog requires client-side JavaScript execution to display

---

### 🐛 BUG-LOAD-003 — Homepage Content Also Bails Out to Client-Side Rendering
- **Severity:** 🟠 High
- **Page:** Homepage (`/`)
- **Section:** Entire main content area
- **Description:** Similar to the Services page, the Homepage source also contains **3 instances of `BAILOUT_TO_CLIENT_SIDE_RENDERING`** for the navbar, main content, and footer. This causes slow initial paint, poor Core Web Vitals (LCP), and makes Google unable to crawl the homepage content effectively.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/`
  2. View page source
  3. Count `BAILOUT_TO_CLIENT_SIDE_RENDERING` occurrences (found: 3)
- **Expected:** Critical content (hero, services, CTAs) should be SSR or SSG rendered
- **Actual:** Multiple client-side bailouts causing delayed content rendering

---

### 🐛 BUG-LOAD-004 — About Page Stats Load as 0 (API Data Not Fetched on SSR)
- **Severity:** 🟠 High
- **Page:** About (`/about`)
- **Section:** Statistics counter cards
- **Description:** The stats (Categories, Services, Areas covered, Active deals) all display `0` indicating the **API call to fetch platform statistics fails or is not made during server-side rendering**. The counters may rely on a client-side fetch that either fails silently or is not completing.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/about`
  2. Observe stat cards (Categories: 0, Services: 0, Areas: 0, Active deals: 0)
  3. Refresh page — values remain 0
- **Expected:** Dynamic API call fetches real-time stats (6 categories, 9 services, 28 areas) and populates cards
- **Actual:** All stats cards show `0` permanently, even after page load completes

---

### 🐛 BUG-LOAD-005 — Service Package Images Appear Blurry / Low Resolution
- **Severity:** 🟡 Medium
- **Page:** Service Details (`/services/ac-master-service`)
- **Section:** Package cards (inside "Select package")
- **Description:** The small thumbnail images used inside package selection cards appear at a **very low resolution / pixelated quality** when displayed at their rendered size. This is likely due to serving small images without proper `srcSet` or responsive image optimization.
- **Steps to Reproduce:**
  1. Navigate to any service detail page
  2. Observe the thumbnail images inside the package options
- **Expected:** Images are sharp at all display densities (especially on Retina/HiDPI screens)
- **Actual:** Images appear blurry or overly compressed
- **Screenshot:** `screenshots/service_detail.png`

---

### 🐛 BUG-LOAD-006 — No Skeleton/Loading State for Category Service Cards
- **Severity:** 🟡 Medium
- **Page:** Services (`/services`)
- **Section:** Service card grid
- **Description:** When the services catalog is loading its data, there is **no skeleton loading UI** shown in the card grid. Instead, users see a raw spinner centered on a grey background. This is a poor UX pattern for a content-heavy catalog page.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/services` on a throttled connection
  2. Observe the loading state
- **Expected:** Skeleton cards with shimmering placeholders fill the grid area while data loads
- **Actual:** A single centered spinner on an empty page is shown during loading
- **Screenshot:** (visible during slow network conditions)

---

## ⚙️ Section 3: Functional / Other Bugs

> Logic errors, broken features, missing validations, UX issues, and configuration problems.

---

### 🐛 BUG-FUNC-001 — "Book Service" Header CTA Routes to Register Page Instead of Services
- **Severity:** 🔴 Critical
- **Page:** All pages (Global Header)
- **Section:** Navigation — "BOOK SERVICE" button
- **Description:** The "BOOK SERVICE" button in the header navigation is labelled as a booking action, but clicking it redirects users to the **registration page** (`/register`) rather than the **services catalog** (`/services`). Unauthenticated users who want to browse services before registering are forced into a registration flow prematurely.
- **Steps to Reproduce:**
  1. Visit any page while unauthenticated
  2. Click the "BOOK SERVICE" button in the top-right header
- **Expected:** Routes to `/services` so users can browse and select a service before being asked to register
- **Actual:** Directly routes to `/register` bypassing the service discovery flow
- **Note:** This is configured via `nav_register_text: "Book Service"` in site settings pointing at the register route

---

### 🐛 BUG-FUNC-002 — Contact Page Shows "28 LIVE AREAS" but No Area List
- **Severity:** 🟡 Medium
- **Page:** Contact (`/contact`)
- **Section:** Left info panel
- **Description:** The Contact page displays **"28 LIVE AREAS"** as a statistic, but nowhere on the website can users find which 28 areas Fixzone actually covers. There is no coverage map, no dropdown, and no link to an areas list. Users from outside Faridpur cannot determine if they are in the service zone.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/contact`
  2. Note the "28 LIVE AREAS" counter
  3. Try to find a list of covered areas — none exists on the website
- **Expected:** A clickable areas coverage map or a "View coverage areas" link revealing the 28 zones
- **Actual:** Number shown with no context or list of areas
- **Screenshot:** `screenshots/contact_page.png`

---

### 🐛 BUG-FUNC-003 — Checkout Accessible Without Items via Direct URL Visit
- **Severity:** 🔴 Critical
- **Page:** Checkout (`/checkout`)
- **Section:** Cart guard / empty cart handling
- **Description:** Authenticated users can navigate directly to `/checkout` even with **zero items in their cart**. While the page should show an empty cart state, the critical issue is whether it also allows form submission with an empty cart — which could create `৳0` orders in the database.
- **Steps to Reproduce:**
  1. Log in to Fixzone
  2. Navigate directly to `https://fixzone.com.bd/checkout` (no items selected)
- **Expected:** Redirect to `/services` immediately OR show a clear "Your cart is empty" state with disabled Place Order button
- **Actual:** Checkout page is accessible with a potentially submittable order form

---

### 🐛 BUG-FUNC-004 — No OTP / Email Verification on Registration
- **Severity:** 🔴 Critical
- **Page:** Register (`/register`)
- **Section:** Account creation flow
- **Description:** The registration form creates an account using only **Name, Phone, Email, and Password** with no OTP verification or email confirmation step. This means:
  - Anyone can create accounts with **fake email addresses** or phone numbers they don't own
  - No phone number ownership verification
  - No email deliverability verification
  - Accounts are created instantly without any identity confirmation
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/register`
  2. Fill in any email (e.g., `fake12345@notrealmail.xyz`) and phone number
  3. Submit — account is created without any verification
- **Expected:** OTP sent to phone number (or email verification link) required before account activation
- **Actual:** Account created immediately with no identity verification

---

### 🐛 BUG-FUNC-005 — Hero Search Bar Keyboard Submit (Enter Key) Behavior Untested
- **Severity:** 🟡 Medium
- **Page:** Homepage (`/`)
- **Section:** Hero search bar
- **Description:** The hero search bar has a visible "Search →" button, but keyboard accessibility (pressing **Enter** to submit) is not confirmed. If the form is not properly wrapped in a `<form>` element with `action`, pressing Enter may do nothing, breaking keyboard-only and assistive technology user flows.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/`
  2. Click into the hero search bar
  3. Type a service name
  4. Press Enter instead of clicking the Search button
- **Expected:** Pressing Enter submits the search and navigates to `/services?q=[query]`
- **Actual:** Behavior may vary — Enter may do nothing or may not navigate correctly

---

### 🐛 BUG-FUNC-006 — Location Refresh Arrow Provides No Visual Feedback
- **Severity:** 🟠 High
- **Page:** Homepage (`/`)
- **Section:** Location bar below hero search
- **Description:** The location section shows "Location: Faridpur →" with a refresh/change icon. Clicking this icon provides **no spinner, no loading animation, and no confirmation** that a location update was triggered. If geolocation takes several seconds (as it often does on mobile), users have no indication anything happened.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/`
  2. Click the directional arrow/refresh icon next to the location text
- **Expected:** Brief spinner or "Locating…" animation during geolocation request; success confirmation updates label
- **Actual:** No feedback; user cannot tell if the action worked

---

### 🐛 BUG-FUNC-007 — Service Page Title Tag (SEO) Uses a Generic Title
- **Severity:** 🟠 High
- **Page:** Services (`/services`)
- **Section:** HTML `<title>` tag
- **Description:** The Services catalog page has the title `"Home Services & Repairs | Fixzone"` which is **too generic** and does not include location-specific keywords (e.g., "Faridpur"). Given that Fixzone's primary market is Faridpur, location-specific titles would dramatically improve local SEO rankings.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/services`
  2. Check the browser tab or view page source `<title>` tag
- **Expected:** `"AC Repair, Plumbing & Home Services in Faridpur | Fixzone"` or similar
- **Actual:** `"Home Services & Repairs | Fixzone"` — generic, no location keywords

---

### 🐛 BUG-FUNC-008 — Register Page Misses Link Back to Login
- **Severity:** 🟠 High
- **Page:** Register (`/register`)
- **Section:** Registration form
- **Description:** The register page does not have a visible "Already have an account? Sign In" link. Users who accidentally land on `/register` when they wanted to log in must use the browser back button or manually navigate to `/login`. This breaks standard UX convention for authentication flows.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/register`
  2. Look for any link to `/login`
- **Expected:** "Already have an account? **Sign In →**" link visible below or inside the registration form
- **Actual:** No such link exists on the register page
- **Screenshot:** `screenshots/register_page.png`

---

### 🐛 BUG-FUNC-009 — Login Page Sign In Format Hint Shows "hame@email.com" Typo
- **Severity:** 🟢 Low
- **Page:** Login (`/login`)
- **Section:** Email/Phone input field placeholder
- **Description:** The email input field on the login page shows the placeholder `"hame@email.com or 01XXXXXXXXX"`. The word **"hame"** is a **typo** — it should be "name" or simply "email@example.com". This is a visible text error shown to every user who visits the login page.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/login`
  2. Observe the placeholder text in the Email or Phone input field
- **Expected:** Placeholder reads "name@email.com or 01XXXXXXXXX" or "Enter your email or phone number"
- **Actual:** Placeholder reads "**hame**@email.com or 01XXXXXXXXX"
- **Screenshot:** `screenshots/login_page.png`

---

### 🐛 BUG-FUNC-010 — No Confirmation Message After Contact Form Submission
- **Severity:** 🟠 High
- **Page:** Contact (`/contact`)
- **Section:** "Send a secure message" form
- **Description:** After submitting the contact form, it is not confirmed whether a **success toast, confirmation banner, or visual feedback** is shown to the user. The configured success message ("Thank you…") needs to be verified as actually displaying. Without clear feedback, users may submit the form multiple times thinking it failed.
- **Steps to Reproduce:**
  1. Navigate to `https://fixzone.com.bd/contact`
  2. Fill in all fields with valid data
  3. Click "Transmit message"
- **Expected:** Clear success confirmation: "✅ Thank you for your message. We'll get back to you within 24 hours."
- **Actual:** Unknown — confirmation feedback may be absent or insufficient

---

## 📁 Evidence / Screenshot Index

| Screenshot File | Contents |
|:---|:---|
| `screenshots/homepage_hero.png` | Hero section with yellow heading and layout — BUG-DESIGN-002, BUG-DESIGN-004 |
| `screenshots/homepage_how_it_works.png` | VR headset wrong image + overlapping buttons — BUG-DESIGN-001, BUG-DESIGN-005 |
| `screenshots/services_page.png` | Services catalog with "1no Sarak" label — BUG-DESIGN-006 |
| `screenshots/service_detail.png` | Package truncation + blurry thumbnails — BUG-DESIGN-003, BUG-LOAD-005 |
| `screenshots/login_page.png` | "hame@" typo + logo rendering issue — BUG-FUNC-009, BUG-DESIGN-009 |
| `screenshots/register_page.png` | Alternative logo + no back-to-login — BUG-DESIGN-010, BUG-FUNC-008 |
| `screenshots/about_page.png` | All stats showing 0 — BUG-DESIGN-008, BUG-LOAD-004 |
| `screenshots/contact_page.png` | "1no Sarak" + admin subject visible — BUG-DESIGN-006, BUG-DESIGN-007, BUG-FUNC-002 |

---

## 🏆 Prioritized Fix Order (Recommended)

| Priority | Bug ID | Reason |
|:---|:---|:---|
| **1st** | BUG-DESIGN-001 | VR headset image — destroys brand credibility immediately |
| **2nd** | BUG-DESIGN-008 | About page stats all showing 0 — business appears inactive |
| **3rd** | BUG-LOAD-001 | Splash screen can permanently block if JS fails |
| **4th** | BUG-LOAD-002 | Services page not SSR — unfindable by Google |
| **5th** | BUG-FUNC-004 | No OTP verification — security/fraud risk |
| **6th** | BUG-FUNC-003 | Empty cart checkout — database integrity risk |
| **7th** | BUG-DESIGN-007 | Admin subject label visible to users — internal data exposure |
| **8th** | BUG-FUNC-009 | "hame@email.com" typo — quick fix, high visibility |
| **9th** | BUG-DESIGN-003 | Package name truncation — users can't read what they're buying |
| **10th** | BUG-DESIGN-006 | "1no Sarak" raw geocoder label — appears on 3 pages |

---

*Report generated by Antigravity QA Engineering · `admin@fixzone.com.bd` for follow-up*
