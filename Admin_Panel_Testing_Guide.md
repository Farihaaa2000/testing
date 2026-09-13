# 🛡️ Admin Panel Testing Guide — Without Sharing Credentials
**Project:** Fixzone Bangladesh (`fixzone.com.bd`)
**Document Version:** 1.0
**Date:** September 2026
**Audience:** Beginners in Software Testing

---

> **⚠️ Important Note**
> You do NOT need to share your admin credentials with anyone to perform testing.
> This guide shows you every testing method available — from tests you can run yourself,
> to tests that only need a test/demo account, to fully automated approaches.

---

## 📚 Table of Contents

1. [Understanding Admin Panel Testing](#1-understanding-admin-panel-testing)
2. [Testing Types Overview](#2-testing-types-overview)
3. [Type 1 — Black-Box Testing (No Login Needed)](#3-type-1--black-box-testing-no-login-needed)
4. [Type 2 — Grey-Box Testing (Limited Access / Test Account)](#4-type-2--grey-box-testing-limited-access--test-account)
5. [Type 3 — Security Testing (Without Credentials)](#5-type-3--security-testing-without-credentials)
6. [Type 4 — Performance & Load Testing](#6-type-4--performance--load-testing)
7. [Type 5 — API Testing (Without UI Login)](#7-type-5--api-testing-without-ui-login)
8. [Type 6 — Accessibility Testing](#8-type-6--accessibility-testing)
9. [Type 7 — Browser Compatibility Testing](#9-type-7--browser-compatibility-testing)
10. [Type 8 — Database & Backend Testing](#10-type-8--database--backend-testing)
11. [Type 9 — Automated UI Testing (With Test Credentials)](#11-type-9--automated-ui-testing-with-test-credentials)
12. [The Safest Way to Give Testers Access](#12-the-safest-way-to-give-testers-access)
13. [Bug Reporting Template](#13-bug-reporting-template)
14. [Tools Summary Table](#14-tools-summary-table)

---

## 1. Understanding Admin Panel Testing

An **admin panel** is a restricted area of a web application that allows authorized users (admins) to manage content, users, orders, settings, etc.

### Why Testing It Is Tricky
- Admin credentials give **full control** over live data — sharing them is dangerous.
- A tester with full access can accidentally **delete real data** or **expose user information**.
- Many bugs are visible **from outside** the admin panel (e.g., effects of admin actions on the public website).

### The Golden Rule
> **Never share your production admin password.** Instead, use one of the safe alternatives described in this guide.

---

## 2. Testing Types Overview

| # | Testing Type | Needs Admin Login? | Who Can Run It |
|---|---|---|---|
| 1 | Black-Box Testing | No | Anyone |
| 2 | Grey-Box Testing | Test account only | Tester with limited access |
| 3 | Security Testing | No (mostly) | Security tester / you |
| 4 | Performance Testing | No | Anyone with a URL |
| 5 | API Testing | Token-based (safe) | Developer / tester |
| 6 | Accessibility Testing | No | Anyone |
| 7 | Browser Compatibility | No | Anyone |
| 8 | Database / Backend | No (indirect) | Developer |
| 9 | Automated UI Testing | Test account only | Developer / tester |

---

## 3. Type 1 — Black-Box Testing (No Login Needed)

**What it is:** Testing the admin panel's **public-facing effects** — what the admin does on the backend should reflect correctly on the public website.

**You do NOT need to log in.** You just check whether admin actions (made by you on your own machine) appear correctly on the website.

---

### How to Do It — Step by Step

#### Step 1: Prepare Your Environment
1. Open two browser windows side-by-side:
   - **Window A** — Your admin panel (logged in as YOU on your own computer)
   - **Window B** — The public-facing Fixzone website (`https://fixzone.com.bd/`)
2. In Window A, make a change (e.g., add a new service, update a price, create a banner).
3. In Window B, refresh the public site and verify the change appeared correctly.

#### Step 2: Test These Admin Actions vs. Public Site
| Admin Action | What to Verify on Public Site |
|---|---|
| Add a new service | Does the service appear in `/services`? |
| Edit a service name/price | Does the new name/price show on the service card? |
| Disable/hide a service | Does it disappear from the public catalog? |
| Add a homepage banner | Does it render on the homepage hero section? |
| Change contact info | Does `/contact` page show updated details? |
| Create a new user account | Can that user log in on the public site? |
| Cancel/change order status | Does customer see updated status on their dashboard? |
| Add a blog post/announcement | Does it appear on the public news/blog section? |

#### Step 3: Check Edge Cases
- Add a service with a **very long name** (100+ characters). Does it break the layout?
- Add a service with **special characters** in the name (e.g., `<script>`, `&`, `"`). Does it display safely?
- Upload an **oversized image** as a service photo. Does the site handle it gracefully?
- Set a price to `0` or negative. Does the public site show it correctly?

#### Step 4: Document Results
For each test:
- PASS — The public site shows the correct result.
- FAIL — Write a bug report (see Section 13).

---

## 4. Type 2 — Grey-Box Testing (Limited Access / Test Account)

**What it is:** Instead of sharing your real admin password, you create a **separate test admin account** with limited permissions — or a **staging/demo environment**.

---

### How to Create a Safe Test Account

#### Option A — Create a Restricted Admin Account
1. Log into your admin panel **yourself**.
2. Go to **Users / Roles / Permissions** settings.
3. Create a new user with role: **"Editor"** or **"Moderator"** (NOT full admin).
4. Set permissions to only what the tester needs (e.g., only view orders, cannot delete users).
5. Share **only this limited account's** credentials with the tester.

#### Option B — Use a Staging/Test Environment
1. Set up a **copy of your website** on a test server (e.g., `staging.fixzone.com.bd` or `test.fixzone.com.bd`).
2. Fill it with **fake/dummy data** (not real customer data).
3. Testers can do anything on this copy — it doesn't affect your real site.
4. Many hosting platforms (Vercel, cPanel, etc.) offer one-click staging environments.

#### Option C — Record Your Own Screen
1. You log in to the admin panel yourself.
2. Use a screen recording tool (OBS Studio, ShareX, Loom).
3. Perform the admin actions and share the video with the tester.
4. The tester watches your actions and tests the **public-facing results**.

---

### Grey-Box Test Checklist

| Test Area | What to Check |
|---|---|
| **Login Page Security** | Does the login page have a CAPTCHA? Does it lock out after 5 wrong attempts? |
| **Dashboard Overview** | Do all stats/numbers load correctly (orders, users, revenue)? |
| **Order Management** | Can orders be viewed, filtered, sorted? Does updating status work? |
| **User Management** | Can users be searched? Does banning a user prevent their login? |
| **Service Management** | Can services be added, edited, deleted? Do changes appear on public site? |
| **Report Generation** | Do reports load? Do exported CSV/PDF files open correctly? |
| **Settings Panel** | Do saved settings actually persist after page refresh? |
| **Notification System** | Are new order notifications appearing in real-time? |

---

## 5. Type 3 — Security Testing (Without Credentials)

**What it is:** Testing whether unauthorized people can access the admin panel or bypass security. This does NOT require you to share your password.

> **WARNING:** Only do security testing on YOUR OWN website. Never do this on someone else's site without written permission.

---

### Security Tests You Can Run (No Password Needed)

#### Test 1 — Direct URL Access (Authorization Test)
1. Open a **new private/incognito browser window** (not logged in).
2. Try to directly visit admin panel URLs, for example:
   - `https://fixzone.com.bd/admin`
   - `https://fixzone.com.bd/admin/dashboard`
   - `https://fixzone.com.bd/admin/users`
   - `https://fixzone.com.bd/admin/orders`
3. **Expected:** You should be **redirected to the login page** — NOT allowed in.
4. **Bug:** If any admin page loads **without being logged in**, that is a critical security vulnerability.

#### Test 2 — SQL Injection on Login Form
1. Go to the admin login page.
2. In the **username** field, type: `' OR '1'='1`
3. In the **password** field, type: `' OR '1'='1`
4. Click Login.
5. **Expected:** Login should **fail** with an error message.
6. **Bug:** If you somehow get logged in, the app is vulnerable to SQL Injection.

#### Test 3 — Brute Force Protection
1. Go to the admin login page.
2. Enter the correct username but a **wrong password** 5–10 times in a row.
3. **Expected:** The account should be **locked out** temporarily, OR a CAPTCHA should appear.
4. **Bug:** If you can keep trying passwords forever with no lockout, it's a brute force vulnerability.

#### Test 4 — HTTPS Check
1. Visit `http://fixzone.com.bd/admin` (with `http`, NOT `https`).
2. **Expected:** The browser should **automatically redirect** to `https://`.
3. **Bug:** If the page loads on `http://` without redirect, data is transmitted insecurely.

#### Test 5 — Default Credentials Check
Try logging in with these common default credentials (they should ALL fail):
| Username | Password |
|---|---|
| admin | admin |
| admin | password |
| admin | 123456 |
| administrator | admin |
| root | root |

**Expected:** All attempts should fail.
**Bug:** If any of these work, change your admin password immediately!

#### Test 6 — Browser Developer Tools Check
1. Open the admin login page.
2. Right-click and select **Inspect** (or press `F12`).
3. Go to the **Network** tab.
4. Try to log in (enter anything, even wrong credentials).
5. Click on the login request in the Network tab.
6. Check if the **password appears in plain text** in the request.
7. **Expected:** Passwords should be sent over HTTPS (encrypted).
8. **Bug:** If the password is visible as plain text in the URL (GET request), that's a security bug.

---

## 6. Type 4 — Performance & Load Testing

**What it is:** Testing how fast the admin panel loads and how well it handles many users at once.

---

### Tool: Google PageSpeed Insights (Free, No Login Needed)

1. Go to: https://pagespeed.web.dev/
2. Enter the admin login page URL (e.g., `https://fixzone.com.bd/admin/login`)
3. Click **Analyze**.
4. Review the scores:
   - **Performance Score** — Should be above 70.
   - **FCP (First Contentful Paint)** — Should be under 2 seconds.
   - **LCP (Largest Contentful Paint)** — Should be under 2.5 seconds.

---

### Tool: GTmetrix (Free, No Login Needed)

1. Go to: https://gtmetrix.com/
2. Enter the admin login page URL.
3. Click **Test your site**.
4. Review the **Grade** (aim for A or B).
5. Note any recommendations (e.g., "compress images", "minify CSS").

---

### Tool: Apache JMeter (Load Testing — Advanced)

**Use case:** Simulate 50, 100, or 500 users accessing the admin panel at once.

**Installation:**
1. Download JMeter from: https://jmeter.apache.org/download_jmeter.cgi
2. Unzip and run `jmeter.bat` (Windows).

**Basic Setup:**
1. Create a **Thread Group** (represents users):
   - Number of Threads (users): `50`
   - Ramp-Up Period: `10` seconds
   - Loop Count: `1`
2. Add an **HTTP Request** sampler:
   - Server Name: `fixzone.com.bd`
   - Path: `/admin/login`
   - Method: `GET`
3. Add a **View Results Tree** listener.
4. Click the **Play** button to run.
5. **Expected:** All requests return `HTTP 200` with response time under 3 seconds.
6. **Bug:** If many requests fail or response time exceeds 5 seconds, there is a performance issue.

---

## 7. Type 5 — API Testing (Without UI Login)

**What it is:** Many admin panels communicate with the server through APIs. You can test these APIs directly without using the browser UI.

---

### Tool: Postman (Free)

**Installation:**
1. Download from: https://www.postman.com/downloads/
2. Install and open.

#### Step 1 — Get an API Token (You Do This Yourself)
1. Log into the admin panel yourself.
2. Go to **Settings → API Keys** (or **Profile → Developer Settings**).
3. Generate a new API key/token.
4. Copy the token.
5. You can share **this token** with a developer/tester (it's safer than a password, and you can revoke it anytime).

#### Step 2 — Test the API in Postman
1. Open Postman.
2. Click **New → HTTP Request**.
3. Enter the API URL, e.g.: `https://fixzone.com.bd/api/admin/orders`
4. Set the method to `GET`.
5. Go to **Headers** tab → Add:
   - Key: `Authorization`
   - Value: `Bearer YOUR_TOKEN_HERE`
6. Click **Send**.
7. **Expected:** Returns a JSON list of orders with `HTTP 200`.
8. **Bug:** If it returns `HTTP 500` (server error) or wrong data.

#### Step 3 — Test API Security
- Send a request **without** the Authorization header.
  - **Expected:** Returns `HTTP 401 Unauthorized`.
- Send a request with a **fake/wrong token**.
  - **Expected:** Returns `HTTP 401` or `HTTP 403 Forbidden`.

---

## 8. Type 6 — Accessibility Testing

**What it is:** Checking whether the admin panel is usable by people with disabilities.

---

### Tool: WAVE (Browser Extension — Free, No Login Needed)

1. Install the WAVE extension:
   - Chrome: https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh
   - Firefox: Available on Firefox Add-ons.
2. Open the admin login page.
3. Click the WAVE icon in your browser toolbar.
4. Review the report:
   - **Red icons** = Errors (must fix).
   - **Yellow icons** = Alerts (should fix).
   - **Green icons** = Good.

---

### Manual Accessibility Checks

| Test | How to Do It | Expected Result |
|---|---|---|
| **Keyboard Navigation** | Press `Tab` to navigate through all fields | Focus should move in logical order (Username → Password → Button) |
| **Enter Key Submit** | Fill in credentials and press `Enter` | Should submit the form |
| **Screen Reader** | Enable Windows Narrator (Win + Ctrl + Enter) and navigate | All fields should be announced with proper labels |
| **Contrast Ratio** | Use https://webaim.org/resources/contrastchecker/ | Text contrast ratio should be at least 4.5:1 |
| **Error Messages** | Submit the login form empty | Error message should be visible and descriptive |

---

## 9. Type 7 — Browser Compatibility Testing

**What it is:** Making sure the admin panel works correctly on all major browsers.

---

### Manual Browser Testing

Test the admin **login page** on each of these browsers:

| Browser | Version to Test |
|---|---|
| Google Chrome | Latest |
| Mozilla Firefox | Latest |
| Microsoft Edge | Latest |
| Safari | Latest (Mac/iOS only) |
| Opera | Latest |

**What to Check on Each Browser:**
- Login form displays correctly (fields are properly sized and aligned).
- Buttons are visible and clickable.
- Fonts and colors render correctly.
- No JavaScript errors (check by pressing `F12` → Console tab).
- Login actually works (enter correct credentials).

---

### Tool: BrowserStack (Online Tool — Free Trial)

1. Go to: https://www.browserstack.com/
2. Sign up for a free trial.
3. Click **Live → Start testing**.
4. Enter the admin login URL.
5. Choose a browser and OS combination (e.g., Chrome on Android, Safari on iPhone).

---

### Responsive Design Testing (Mobile View)

1. Open the admin login page in Chrome.
2. Press `F12` to open DevTools.
3. Click the **Toggle Device Toolbar** icon or press `Ctrl + Shift + M`.
4. Use the dropdown to test on different device sizes:
   - iPhone SE (375px wide)
   - iPad (768px wide)
   - Desktop (1280px wide)
5. **Expected:** The admin panel should be usable on all sizes.
6. **Bug:** If fields overlap, buttons are cut off, or text is unreadable on mobile.

---

## 10. Type 8 — Database & Backend Testing

**What it is:** Verifying that actions in the admin panel actually save correctly to the database.

---

### Indirect Database Testing (No Direct DB Access Needed)

| Admin Action | How to Verify DB Persistence |
|---|---|
| Create a new service | Refresh the page after creating. Does it still appear? |
| Edit an order status | Log out and back in. Is the status still changed? |
| Delete a user | Try to log in as that deleted user — should fail. |
| Change site settings | Refresh the browser after saving. Are settings still applied? |
| Upload a file/image | Close and reopen the admin panel. Is the image still there? |

---

### Tool: phpMyAdmin (Direct DB — For Developers Only)

If you have direct database access (e.g., through cPanel → phpMyAdmin):
1. Log into phpMyAdmin.
2. Navigate to the relevant table (e.g., `services`, `orders`, `users`).
3. After making a change in the admin panel, click **Refresh** in phpMyAdmin.
4. **Expected:** The change appears in the database row.
5. **Bug:** If the admin panel says "Saved" but the database hasn't changed.

> **Note:** Never share phpMyAdmin access with external testers. Do this verification yourself.

---

## 11. Type 9 — Automated UI Testing (With Test Credentials)

**What it is:** Writing code that automatically clicks through the admin panel and verifies everything works. Run this with a dedicated **test account** (not your real admin account).

---

### Tool: Selenium IDE (Beginner-Friendly, No Coding Needed)

**Selenium IDE** lets you **record** your actions in the browser and replay them automatically.

#### Installation
1. Install the Chrome extension: https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd
2. Open Chrome and click the Selenium IDE icon.

#### Recording a Test
1. Click **Create a new project** → Name it `Fixzone Admin Tests`.
2. Click **Record a new test** → Name it `Admin Login Test`.
3. Enter the admin URL and click **Start Recording**.
4. Selenium IDE will record everything you do:
   - Click the username field → type your **test account** username.
   - Click the password field → type your **test account** password.
   - Click the Login button.
5. Click **Stop Recording**.
6. Click **Run** to replay the test automatically.
7. **Pass:** Green checkmarks next to each step.
8. **Fail:** Red X with a description of what went wrong.

---

### Tool: Playwright (Advanced — For Developers)

```javascript
// test_admin_login.spec.js
const { test, expect } = require('@playwright/test');

test('Admin login should succeed with valid credentials', async ({ page }) => {
  await page.goto('https://fixzone.com.bd/admin/login');
  await page.fill('#username', 'test_admin@fixzone.com.bd');
  await page.fill('#password', 'TestPassword123!');
  await page.click('button[type="submit"]');
  await expect(page).toHaveURL(/.*dashboard/);
  await expect(page.locator('h1')).toContainText('Dashboard');
});

test('Admin login should fail with wrong credentials', async ({ page }) => {
  await page.goto('https://fixzone.com.bd/admin/login');
  await page.fill('#username', 'wronguser@fixzone.com.bd');
  await page.fill('#password', 'WrongPassword!');
  await page.click('button[type="submit"]');
  await expect(page).toHaveURL(/.*login/);
  await expect(page.locator('.error-message')).toBeVisible();
});
```

**To Run Playwright Tests:**
```bash
# Install Playwright
npm install -g @playwright/test

# Run tests
npx playwright test test_admin_login.spec.js

# View results in HTML report
npx playwright show-report
```

---

## 12. The Safest Way to Give Testers Access

### Step-by-Step Safe Access Protocol

1. **Create a dedicated test environment** — Use a staging server, not production.
2. **Create a restricted test account** — With only the permissions needed for testing.
3. **Use a temporary password** — Set it to expire after testing is done.
4. **Use a password manager** — Share credentials via 1Password, Bitwarden, or LastPass (do NOT send via WhatsApp or email).
5. **Enable 2FA** — Even for test accounts, enable two-factor authentication.
6. **Monitor the session** — Log all actions the test account takes (most admin panels have audit logs).
7. **Revoke access after testing** — Delete or disable the test account when done.

### Never Do This
- Never share credentials via WhatsApp, SMS, or email.
- Never share your main/root admin password.
- Never allow external testers to access your production database.
- Never store passwords in a Google Doc or spreadsheet.

---

## 13. Bug Reporting Template

```
Bug Report
---
Bug ID:         [e.g., BUG-ADMIN-001]
Date Found:     [e.g., 2026-09-13]
Found By:       [Your name]
Testing Type:   [e.g., Security Testing / Black-Box Testing]
Severity:       [Critical / High / Medium / Low]
Status:         [Open]

Title:
[Short description]

Environment:
- URL:          [e.g., https://fixzone.com.bd/admin/users]
- Browser:      [e.g., Google Chrome 127]
- OS:           [e.g., Windows 11]
- Device:       [e.g., Desktop / Samsung Galaxy S21]

Steps to Reproduce:
1. [Step 1]
2. [Step 2]
3. [Observe what happens]

Expected Result:
[What should happen]

Actual Result:
[What actually happened]

Screenshot/Video:
[Attach file or paste link]

Notes:
[Any additional context]
```

---

## 14. Tools Summary Table

| Tool | Purpose | Cost | Requires Login? | Link |
|---|---|---|---|---|
| **Google PageSpeed** | Page performance score | Free | No | https://pagespeed.web.dev |
| **GTmetrix** | Speed & optimization report | Free tier | No | https://gtmetrix.com |
| **WAVE** | Accessibility checker | Free | No | https://wave.webaim.org |
| **BrowserStack** | Cross-browser live testing | Free trial | No | https://browserstack.com |
| **Postman** | API testing | Free | No (uses tokens) | https://postman.com |
| **Selenium IDE** | Record & replay UI tests | Free | Test account | https://www.selenium.dev/selenium-ide/ |
| **Playwright** | Automated browser testing | Free | Test account | https://playwright.dev |
| **Apache JMeter** | Load & performance testing | Free | No | https://jmeter.apache.org |
| **WebAIM Contrast** | Color contrast checker | Free | No | https://webaim.org/resources/contrastchecker/ |
| **Bitwarden** | Secure credential sharing | Free/Paid | N/A | https://bitwarden.com |

---

## Quick Start Checklist for Beginners

Start here if you are completely new:

- [ ] **Day 1:** Run Black-Box Testing (Section 3) — No setup required.
- [ ] **Day 1:** Run Security Tests 1–5 (Section 5) — Takes 30 minutes.
- [ ] **Day 2:** Install WAVE extension and run Accessibility Testing (Section 6).
- [ ] **Day 2:** Test the login page on Chrome, Firefox, and Edge (Section 7).
- [ ] **Day 3:** Run GTmetrix and PageSpeed on the admin login URL (Section 6).
- [ ] **Day 3:** Install Postman and test one API endpoint (Section 7).
- [ ] **Day 4:** Record a basic test with Selenium IDE (Section 11).
- [ ] **Ongoing:** Report all bugs using the Bug Report Template (Section 13).

---

*Document prepared for Fixzone Bangladesh QA Process. All testing should be performed on the designated test environment. Never test on production with destructive operations.*
