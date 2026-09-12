# 🧪 Software Test Case Specification Document — Fixzone Bangladesh
**Target Application:** [Fixzone.com.bd](https://fixzone.com.bd/)  
**Application Type:** On-Demand Home Services & Repair Marketplace Web Application  
**Target Platform:** Web (Desktop, Tablet, Mobile Browsers)  
**Primary Location / Hub:** Faridpur Sadar, Bangladesh  
**Document Version:** 1.0  
**Date:** September 2026  
**Document Author:** Antigravity QA Engineering  

---

## 📋 Executive Summary

This document contains a comprehensive suite of manual and automated test cases covering end-to-end functionality, UI/UX, business logic, cross-browser compatibility, security, and performance for **Fixzone (`https://fixzone.com.bd/`)**.

### Test Suite Structure & Modules Covered:
1. **Module 01: Header, Navigation & Global Location Context**
2. **Module 02: Homepage Hero, Search & Service Discovery**
3. **Module 03: Services Catalog & Category Filtering (`/services`)**
4. **Module 04: Service Details, Interactive Packages & Dynamic Cart (`/services/[slug]`)**
5. **Module 05: Authentication & Authorization (`/login`, `/register`, `/forgot-password`)**
6. **Module 06: Checkout Flow, Distance-Based Conveyance & Order Placement (`/checkout`)**
7. **Module 07: Customer Dashboard & Order Tracking (`/customer-dashboard`)**
8. **Module 08: Contact & Support Portal (`/contact`)**
9. **Module 09: Informational & Policy Pages (`/about`, `/privacy`, `/terms`, `/help`)**
10. **Module 10: Cross-Browser, Responsive UI & Mobile Usability**
11. **Module 11: Security, Vulnerability & Input Sanitization**
12. **Module 12: SEO, Schema Markup & Page Performance**

---

## 🏷️ Test Case Priority & Severity Legend

| Severity | Definition |
| :--- | :--- |
| **Critical (P0)** | Blocks core business workflow (e.g., checkout failure, auth breakdown, crash). Must be fixed immediately. |
| **High (P1)** | Major feature failure or calculation error (e.g., pricing inaccuracy, conveyance failure, search broken). |
| **Medium (P2)** | Normal feature defect, layout mismatch, or non-blocking validation issue. |
| **Low (P3)** | Minor cosmetic, typo, or minor micro-interaction quirk. |

---

## 📑 Detailed Test Case Specifications

---

### 1. Module 01: Header, Navigation & Global Location Context

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-NAV-001** | Verify Fixzone Logo Navigation | Browser open on any subpage (e.g. `/services`, `/about`) | 1. Click on the Fixzone logo in the header. | N/A | User is immediately routed back to the Homepage (`/`). Logo renders crisp without distortion. | P2 |
| **TC-NAV-002** | Verify Top Navigation Links Redirection | Homepage loaded | 1. Click `Home`.<br>2. Click `Services`.<br>3. Click `About`.<br>4. Click `Contact`. | N/A | Each navigation link redirects to `/`, `/services`, `/about`, and `/contact` respectively with active state highlighted. | P1 |
| **TC-NAV-003** | Verify Global Location Indicator Display | User visits site | 1. Observe the location badge in the top bar. | Geolocation permissions (Granted / Denied) | Displays detected location (e.g. `Location: Faridpur` or selected area). If permission denied, defaults to configured hub (`Faridpur Sadar`). | P1 |
| **TC-NAV-004** | Verify "Refresh detected location" Trigger | Location shown | 1. Click the refresh button next to location. | N/A | Triggers browser geolocation re-prompt or refreshes coordinate cache with smooth spinner/feedback. | P2 |
| **TC-NAV-005** | Verify "Sign In" Button Navigation | User is unauthenticated | 1. Click `Sign In` button in header. | N/A | Redirects user to `/login` page with proper clean UI state. | P1 |
| **TC-NAV-006** | Verify "Book Service" CTA Button Navigation | User on homepage/header | 1. Click `Book Service` CTA button in header. | N/A | Directs user to the services catalog (`/services`) or registration depending on configuration. | P1 |
| **TC-NAV-007** | Verify Authenticated User State in Header | User logged in | 1. Log in with valid credentials.<br>2. Observe header. | Valid customer session | `Sign In` is replaced by Customer Profile / Avatar / Access Hub dropdown with Dashboard and Logout options. | P1 |

---

### 2. Module 02: Homepage Hero, Search & Service Discovery

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-HOME-001** | Verify Hero Search with Valid Keywords | Homepage loaded | 1. Type service name into hero search bar.<br>2. Press Enter or click `Search` button. | "AC Master", "Plumbing", "Gas refill" | Redirects to `/services?q=[keyword]` displaying filtered matching service cards. | P0 |
| **TC-HOME-002** | Verify Hero Search with Empty Input | Homepage loaded | 1. Leave search bar empty.<br>2. Click `Search` button. | Empty string `""` | Redirects to `/services` displaying all services or shows inline tooltip requesting input. | P2 |
| **TC-HOME-003** | Verify Hero Search with Non-Existent Query | Homepage loaded | 1. Type non-existent query into search bar.<br>2. Click `Search`. | "XYZ999UnknownItem" | Navigates to `/services?q=XYZ999UnknownItem` displaying clean "No services found" placeholder with "Reset filters" option. | P2 |
| **TC-HOME-004** | Verify Hero Slide Pagination Controls | Homepage loaded | 1. Observe automatic carousel transitions.<br>2. Click on pagination dots 1, 2, 3, 4. | N/A | Slides transition smoothly with matching backdrop animations and updated promotional content. | P3 |
| **TC-HOME-005** | Verify Featured Services Carousel Navigation | Homepage loaded | 1. Click the Right Carousel Arrow (`>`).<br>2. Click the Left Carousel Arrow (`<`).<br>3. Click `Explore All` link. | N/A | Carousel scrolls to reveal next/previous service cards. `Explore All` navigates to `/services`. | P2 |
| **TC-HOME-006** | Verify Featured Service Card Click | Homepage loaded | 1. Click on a featured service card (e.g. AC Master Service). | N/A | Navigates directly to the specific service details page (`/services/ac-master-service`). | P1 |
| **TC-HOME-007** | Verify Floating "Back to Top" Button | User scrolled down | 1. Scroll 1000px down on Homepage.<br>2. Click floating arrow-up button in bottom-right. | N/A | Button smoothly animates page scroll back to `Y: 0` (top) and then gracefully hides itself. | P2 |
| **TC-HOME-008** | Verify Embedded Google Map & Contact Details | Homepage bottom | 1. Scroll to the footer section.<br>2. Inspect address, phone (`+880 1767 100434`), email, and embedded map. | N/A | Interactive map renders centered on East Khabaspur, Faridpur. Phone link initiates tel prompt; email link opens mailto. | P2 |

---

### 3. Module 03: Services Catalog & Category Filtering (`/services`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-SRV-001** | Verify Services Catalog Default Load | User navigates to `/services` | 1. Load `/services`.<br>2. Observe category count badge, service count badge, and service grid. | N/A | Catalog loads active services (e.g. AC Master, Foam Wash, Jet Wash, Gas Refill, Maintenance, Troubleshooting). Area badge displays current serving location. | P1 |
| **TC-SRV-002** | Verify Category Filter Selection | `/services` loaded | 1. Click on category `AC Cleaning Services`.<br>2. Click on `AC Repair Service`.<br>3. Click on `AC Installation & Shifting`.<br>4. Click on `Professional Cleaning Service`. | Category clicks | Service grid instantly filters to only show services belonging to selected category; category counts match items displayed. | P1 |
| **TC-SRV-003** | Verify Live Search Input in Catalog | `/services` loaded | 1. Type "Foam" into search input.<br>2. Type "Troubleshooting".<br>3. Clear input. | "Foam", "Troubleshooting" | Cards dynamically filter in real-time or upon keyup without page reload. Clearing input restores all category items. | P1 |
| **TC-SRV-004** | Verify Service Card Elements Display | `/services` loaded | 1. Inspect any service card. | N/A | Card displays: Service Image, Category Name, Service Title, Description summary, Estimated Duration (e.g. `3-4 Hours`), Discount Tag (e.g. `20% off`), Starting Price in BDT (`From ৳ 1,500`), and `Details ->` CTA. | P1 |
| **TC-SRV-005** | Verify "Details ->" Link Navigation | `/services` loaded | 1. Click `Details ->` on `AC Master Service`. | N/A | Redirects to `/services/ac-master-service` with appropriate URL slug and loaded content. | P1 |

---

### 4. Module 04: Service Details, Interactive Packages & Dynamic Cart (`/services/[slug]`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-DET-001** | Verify Service Details Breadcrumb | Service page loaded | 1. Inspect breadcrumb navigation.<br>2. Click `Services` breadcrumb link. | N/A | Breadcrumb shows `Home > Services > [Service Name]`. Clicking `Services` navigates to `/services`. | P2 |
| **TC-DET-002** | Verify Image Gallery Thumbnail Switching | Service page loaded | 1. Click thumbnail `View image 2`.<br>2. Click thumbnail `View image 3`.<br>3. Click thumbnail `View image 1`. | N/A | Main large preview swaps smoothly to selected thumbnail image without broken assets or layout jumps. | P2 |
| **TC-DET-003** | Verify Package Quantity Increment & Decrement | Service page loaded | 1. Click `+` on package "Indoor Only (৳1,200)".<br>2. Click `+` again (Qty = 2).<br>3. Click `-` on package (Qty = 1).<br>4. Click `-` again (Qty = 0). | N/A | Quantity updates dynamically. Subtotal and Cart items count update instantly. Cannot decrement below 0. | P0 |
| **TC-DET-004** | Verify Multiple Package Selection Calculation | Service page loaded | 1. Select Qty 1 of "Indoor Only" (৳1,200).<br>2. Select Qty 2 of "Indoor + Outdoor Unit" (৳1,560 each). | Qty 1 (৳1200) + Qty 2 (৳3120) | Dynamic sidebar TOTAL displays `৳ 4,320` and selected items shows `3 items selected`. | P0 |
| **TC-DET-005** | Verify Conveyance Cost Estimate in Sidebar | Service page loaded | 1. Check conveyance cost note in cart sidebar. | User GPS / Location context | Displays estimated distance and conveyance (e.g., `From ৳0, ~0 km from Fixzone, Faridpur Sadar (GPS estimate)`). | P1 |
| **TC-DET-006** | Verify "Continue to checkout" Button State | Service page loaded | 1. Keep selected items = 0.<br>2. Observe checkout button.<br>3. Add 1 package.<br>4. Observe checkout button. | Qty = 0, then Qty = 1 | Button is disabled/inactive when Qty = 0. Button becomes active/clickable when Qty ≥ 1. | P0 |
| **TC-DET-007** | Verify Details Tabs Switching | Service page loaded | 1. Click `Specification` tab.<br>2. Click `Description` tab.<br>3. Click `Questions` tab.<br>4. Click `Reviews` tab. | N/A | Tab content swaps correctly without reload. Empty states ("No questions added from admin yet", "No reviews yet") render cleanly if no entries exist. | P2 |
| **TC-DET-008** | Verify "Similar Service" Recommendations Widget | Service page loaded | 1. Inspect sidebar "Similar Service" section.<br>2. Click on a recommended service item. | N/A | Displays related services in the same category. Clicking one navigates to its corresponding details page. | P2 |

---

### 5. Module 05: Authentication & Authorization (`/login`, `/register`, `/forgot-password`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-AUTH-001** | Verify Login with Valid Registered Email | User at `/login` | 1. Enter valid email.<br>2. Enter correct password.<br>3. Click `SIGN IN TO YOUR ACCOUNT`. | Email: `user@fixzone.test`<br>Password: `ValidPass123` | Login successful. Session token saved; user redirected to dashboard or callback URL. | P0 |
| **TC-AUTH-002** | Verify Login with Valid Phone Number | User at `/login` | 1. Enter registered phone number.<br>2. Enter correct password.<br>3. Click `SIGN IN TO YOUR ACCOUNT`. | Phone: `01712345678`<br>Password: `ValidPass123` | Login successful; authenticated session created. | P0 |
| **TC-AUTH-003** | Verify Login with Incorrect Password | User at `/login` | 1. Enter registered email/phone.<br>2. Enter invalid password.<br>3. Click `SIGN IN`. | Password: `WrongPassword99` | Error toast/alert displayed: "Invalid email/phone or password". User remains on login page; form not cleared unsafely. | P1 |
| **TC-AUTH-004** | Verify Login Password Visibility Toggle | User at `/login` | 1. Type password.<br>2. Click the Eye icon toggle button. | Password: `SecretPassword` | Field type switches from `password` (masked dots) to `text` (plain text) and back when clicked again. | P2 |
| **TC-AUTH-005** | Verify Customer Registration with Valid Data | User at `/register` | 1. Enter Full Name.<br>2. Enter valid BD Phone Number.<br>3. Enter valid Email.<br>4. Enter Password (≥ 6-8 chars).<br>5. Click `CREATE CUSTOMER ACCOUNT`. | Name: "Rony Ahmed"<br>Phone: "01767100434"<br>Email: "rony.ahmed@example.com"<br>Pass: "SecurePass@2026" | Account created successfully. User logged in automatically and redirected to customer onboarding / dashboard. | P0 |
| **TC-AUTH-006** | Verify Registration with Existing Email/Phone | User at `/register` | 1. Enter already registered email or phone.<br>2. Submit form. | Duplicate email/phone | Validation error: "An account with this email or phone number already exists." | P1 |
| **TC-AUTH-007** | Verify Registration Form Validation & Empty Fields | User at `/register` | 1. Leave fields blank.<br>2. Click `CREATE CUSTOMER ACCOUNT`. | Empty fields | Client-side HTML5 & React validation errors indicate required fields (`Full name`, `Contact Number`, `Email`, `Password`). | P1 |
| **TC-AUTH-008** | Verify Registration Phone Format Validation | User at `/register` | 1. Enter invalid phone format (e.g. letters or < 11 digits). | Phone: `12345` or `017abcd` | Inline error: "Please enter a valid 11-digit Bangladeshi mobile number (01XXXXXXXXX)". | P1 |
| **TC-AUTH-009** | Verify "Forgot password?" Link Redirection | User at `/login` | 1. Click `Forgot password?` link. | N/A | Navigates to `/forgot-password` with reset instructions / OTP verification prompt. | P1 |
| **TC-AUTH-010** | Verify Auth Guard for Protected Pages | Unauthenticated user | 1. Attempt to navigate directly to `/checkout` or `/customer-dashboard`. | Direct URL visit | Automatically intercepted and redirected to `/login?callback=/checkout` with callback parameter preserved. | P0 |
| **TC-AUTH-011** | Verify Redirect to Callback URL After Login | Redirected to `/login?callback=/checkout` | 1. Enter valid credentials.<br>2. Click `SIGN IN`. | Valid credentials | After authentication, user is redirected directly to `/checkout` with their selected cart items intact. | P0 |

---

### 6. Module 06: Checkout Flow, Distance-Based Conveyance & Order Placement (`/checkout`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-CHK-001** | Verify Checkout Page Load with Selected Items | User logged in with items in cart | 1. Navigate to `/checkout`.<br>2. Inspect order summary. | AC Master Service (Qty 1 = ৳1,200) | Displays selected items, quantity, item prices, and subtotal accurately. | P0 |
| **TC-CHK-002** | Verify Empty Cart Checkout Prevention | User logged in with empty cart | 1. Navigate to `/checkout` with 0 items. | Cart = 0 | Displays empty cart prompt with button "Browse Services" linking to `/services`. Cannot place order. | P1 |
| **TC-CHK-003** | Verify Service Address & Area Selection | User on `/checkout` | 1. Enter street address.<br>2. Select Area / Thana (e.g. Faridpur Sadar).<br>3. Pick pin on interactive map. | Street: "East Khabaspur, Road 2", Lat/Lng coordinates | Address fields populated; map pin accurately registers latitude & longitude. | P0 |
| **TC-CHK-004** | Verify Conveyance Fee Calculation (Within Free Radius) | User on `/checkout` | 1. Set service location within 3 km of Fixzone Faridpur Hub (23.597688, 89.829964). | Distance: 2.1 km | Conveyance fee calculates to `৳ 0` (Free within 3 km radius). | P1 |
| **TC-CHK-005** | Verify Conveyance Fee Calculation (Beyond Free Radius) | User on `/checkout` | 1. Set location 10 km away from Hub. | Distance: 10 km (Base: ৳100 + 7km × ৳15) | Conveyance calculates accurately based on configured road distance formula: `Base Fee + (Distance - Free Radius) * Rate`. | P0 |
| **TC-CHK-006** | Verify Conveyance Maximum Fee Cap | User on `/checkout` | 1. Set service location > 35 km away. | Distance: 40 km | Conveyance fee is capped at configured maximum limit (`৳ 500`). | P1 |
| **TC-CHK-007** | Verify Conveyance Fallback without GPS | User on `/checkout` | 1. Enter manual address without granting GPS map pin. | Manual text address | Applies configured fallback flat conveyance fee (`৳ 80`). | P1 |
| **TC-CHK-008** | Verify Schedule Date & Time Slot Picker | User on `/checkout` | 1. Select booking date (Tomorrow).<br>2. Select available time slot (e.g. `10:00 AM - 12:00 PM`). | Valid future date & slot | Selected schedule is saved and reflected in order summary. Cannot select past dates. | P0 |
| **TC-CHK-009** | Verify VAT / Tax Calculation | User on `/checkout` | 1. Inspect VAT line item in checkout summary. | Subtotal = ৳1,000, VAT = 5% | 5% exclusive VAT calculates to `৳ 50`. Total = Subtotal (৳1000) + Conveyance + VAT (৳50). | P0 |
| **TC-CHK-010** | Verify Payment Method Selection (Cash on Delivery) | User on `/checkout` | 1. Select `Cash on Delivery (COD)` radio option.<br>2. Click `Place Order`. | All required fields filled | Order placed successfully; redirect to Order Confirmation page with unique Order ID (e.g. `#FXZ-89214`). | P0 |
| **TC-CHK-011** | Verify Digital Payment Methods Disabled / Enabled States | User on `/checkout` | 1. Inspect payment options: bKash, Nagad, Rocket, Cards. | Payment gateway settings | Disabled methods are visibly greyed out with "Coming Soon" or active methods redirect to MFS gateway. | P1 |
| **TC-CHK-012** | Verify Mandatory Field Validation on Order Placement | User on `/checkout` | 1. Leave Phone Number or Address blank.<br>2. Click `Place Order`. | Missing phone/address | Form highlights missing fields with red borders and inline validation messages. Order is not submitted. | P0 |

---

### 7. Module 07: Customer Dashboard & Order Tracking (`/customer-dashboard`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-DASH-001** | Verify Customer Dashboard Overview | Logged in as customer | 1. Navigate to `/customer-dashboard`. | Valid customer session | Displays Customer Name, Contact info, Active Bookings count, and Past Orders. | P1 |
| **TC-DASH-002** | Verify Order Status Lifecycle Display | Customer has active order | 1. Check order status on dashboard. | Order Status: `Pending` / `Confirmed` / `Technician Assigned` / `In Progress` / `Completed` / `Cancelled` | Status badge displays correct state with appropriate color badge (Yellow: Pending, Blue: In Progress, Green: Completed). | P0 |
| **TC-DASH-003** | Verify Order Invoice Download / View | Customer has completed order | 1. Click `View Invoice` or `Download PDF`. | Completed Order ID | Displays detailed invoice breakdown (Services, Conveyance, VAT, Total BDT, Fixzone contact info). | P1 |
| **TC-DASH-004** | Verify Profile Information Update | Customer on dashboard | 1. Edit Name, Alternate Phone, or Default Address.<br>2. Click `Save Changes`. | Updated profile details | Success notification shown; updated data persists across sessions. | P2 |
| **TC-DASH-005** | Verify Customer Logout | Customer logged in | 1. Click `Logout` / `Sign Out` button. | N/A | Session is securely cleared; user redirected to Homepage (`/`); protected pages no longer accessible. | P0 |

---

### 8. Module 08: Contact & Support Portal (`/contact`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-CNT-001** | Verify Contact Page Load & Metadata | User visits `/contact` | 1. Inspect page elements: Desk status, Response time indicator, Topic tabs, Form fields. | N/A | Shows "Desk online", "Typically < 24h", live area context (`1no Sarak`), and full contact coordinates. | P2 |
| **TC-CNT-002** | Verify Contact Topic Selector Switching | User at `/contact` | 1. Click topic tabs: `General`, `Booking`, `Billing`, `Partnership`, `Press`. | Tab selections | Active tab highlights; message context or subject updates accordingly. | P2 |
| **TC-CNT-003** | Verify Contact Form Message Character Counter | User at `/contact` | 1. Type characters in `Message` textarea.<br>2. Observe counter. | 50 characters typed | Character counter displays `50 / 2000` dynamically and prevents exceeding 2000 characters. | P2 |
| **TC-CNT-004** | Verify Contact Form Submission with Valid Data | User at `/contact` | 1. Enter Name: "Fariha Rahman".<br>2. Enter Email: "fariha@test.com".<br>3. Enter Phone: "01711223344".<br>4. Enter Message: "Need AC duct cleaning for office."<br>5. Click `Transmit message`. | Valid inputs | Success confirmation displayed: "Thank you for contacting Fixzone. Our team will get back to you shortly." Form resets. | P1 |
| **TC-CNT-005** | Verify Contact Form Validation on Invalid Email | User at `/contact` | 1. Enter invalid email (e.g. `user@test`).<br>2. Click `Transmit message`. | Invalid email syntax | Displays email validation error: "Please enter a valid email address." Form not submitted. | P1 |
| **TC-CNT-006** | Verify Direct Phone & Email Action Links | User at `/contact` | 1. Click telephone link `+880 1767 100434`.<br>2. Click email link `admin@fixzone.com.bd`. | N/A | Phone link opens device dialer (`tel:+8801767100434`); email link triggers default mail client (`mailto:admin@fixzone.com.bd`). | P2 |

---

### 9. Module 09: Informational & Policy Pages (`/about`, `/privacy`, `/terms`, `/help`)

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-INFO-001** | Verify About Us Page Content & Stats | User visits `/about` | 1. Inspect statistics counters and company mission statement. | N/A | Stats cards (Categories, Services, Areas covered, Active deals) render correctly. CTA links route to `/services` and `/contact`. | P3 |
| **TC-INFO-002** | Verify Privacy Policy & Terms Pages Load | User navigates to `/privacy` & `/terms` | 1. Open `/privacy` and `/terms`. | N/A | Legal policies on customer data protection, booking cancellation, and refunds load cleanly with HTTP 200. | P2 |
| **TC-INFO-003** | Verify 404 Custom Error Page | Browser open | 1. Navigate to a non-existent URL: `https://fixzone.com.bd/random-page-12345`. | Invalid URL | Clean custom 404 page renders ("404: This page could not be found") with a button to return to Homepage. | P2 |

---

### 10. Module 10: Cross-Browser, Responsive UI & Mobile Usability

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-RSP-001** | Verify Mobile Viewport Layout (375px - 430px) | Chrome DevTools Mobile Mode (iPhone 14 / Pixel 7) | 1. Load Homepage, Services, Details, and Checkout on mobile screen width. | 390px × 844px | Navigation collapses to responsive hamburger drawer. Sticky cart bar/buttons adapt to screen bottom without overlapping content. | P1 |
| **TC-RSP-002** | Verify Mobile Drawer Navigation Menu | Mobile viewport | 1. Tap hamburger menu icon.<br>2. Verify menu items.<br>3. Tap a link or close button. | Mobile device | Drawer slides out smoothly with backdrop blur. Tapping any link navigates and closes drawer. | P1 |
| **TC-RSP-003** | Verify Tablet Viewport Layout (768px - 1024px) | iPad / Tablet viewport | 1. Load `/services` and `/services/[slug]`. | 768px × 1024px | Grid switches to 2 columns; package selection and cart sidebar adapt gracefully without horizontal scrollbars. | P2 |
| **TC-RSP-004** | Verify Cross-Browser Compatibility (Chrome, Firefox, Safari, Edge) | Modern web browsers | 1. Execute booking and auth flows across Google Chrome, Mozilla Firefox, Apple Safari, and Microsoft Edge. | All major browsers | Layouts, gradients, CSS backdrop filters, and JavaScript state behave consistently across all browsers. | P1 |

---

### 11. Module 11: Security, Vulnerability & Input Sanitization

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-SEC-001** | Verify HTTPS Enforcement & SSL Certificate | Browser address bar | 1. Navigate to `http://fixzone.com.bd/`. | HTTP request | Automatically redirects to secure `https://fixzone.com.bd/` with valid SSL certificate. | P0 |
| **TC-SEC-002** | Verify Cross-Site Scripting (XSS) Prevention in Forms | Contact / Search / Register forms | 1. Inject script payload into search, contact message, and full name fields.<br>2. Submit form. | `<script>alert('XSS')</script>`, `<img src=x onerror=alert(1)>` | Input is properly sanitized and HTML-encoded. Script does not execute in DOM or alerts. | P0 |
| **TC-SEC-003** | Verify SQL Injection (SQLi) Prevention | Search & Login inputs | 1. Input SQL injection strings into login and search fields.<br>2. Submit. | `' OR '1'='1' --`, `' UNION SELECT null, username, password FROM users --` | Queries use parameterized statements / ORM; no internal database errors or bypasses occur. | P0 |
| **TC-SEC-004** | Verify Rate Limiting on Authentication & Contact APIs | Postman / API Client | 1. Send 50 rapid POST requests to `/api/auth/login` or `/api/contact`. | Rapid burst requests | Server responds with HTTP 429 Too Many Requests after threshold is reached, protecting against brute-force attacks. | P1 |
| **TC-SEC-005** | Verify Secure Storage of Auth Tokens & Cookies | User logged in | 1. Inspect browser Application tab (Cookies, LocalStorage). | Auth session | Sensitive auth cookies use `HttpOnly`, `Secure`, and `SameSite=Lax/Strict` flags. Passwords never stored in plaintext. | P0 |

---

### 12. Module 12: SEO, Schema Markup & Page Performance

| Test Case ID | Test Scenario | Preconditions | Test Steps | Test Data / Input | Expected Result | Severity |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-SEO-001** | Verify JSON-LD Structured Data Schema | Homepage & Services page | 1. Inspect page source `<script type="application/ld+json">`. | N/A | Contains valid `Organization`, `LocalBusiness` (Fixzone, East Khabaspur, Faridpur, geo coordinates: 23.597688, 89.829964), and `WebSite` schemas. | P2 |
| **TC-SEO-002** | Verify OpenGraph (OG) and Twitter Meta Tags | Any page | 1. Inspect `<meta property="og:title">`, `og:image`, `twitter:card`. | N/A | OG tags contain accurate titles, descriptions, and valid 1200x630 banner images for rich social previews. | P2 |
| **TC-SEO-003** | Verify Page Load Speed & Core Web Vitals | Lighthouse / PageSpeed | 1. Run Lighthouse audit on Desktop & Mobile. | N/A | TTFB < 200ms, LCP < 2.5s, CLS < 0.1, Overall Performance Score ≥ 85-90+. | P2 |

---

## 📊 Test Case Summary Matrix

| Module No. | Module Name | Total Test Cases | Critical (P0) | High (P1) | Medium (P2) | Low (P3) |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: |
| **01** | Header, Navigation & Location Context | 7 | 0 | 4 | 3 | 0 |
| **02** | Homepage Hero, Search & Discovery | 8 | 1 | 1 | 5 | 1 |
| **03** | Services Catalog & Category Filters | 5 | 0 | 4 | 1 | 0 |
| **04** | Service Details & Interactive Packages | 8 | 3 | 1 | 4 | 0 |
| **05** | Authentication & Authorization | 11 | 6 | 4 | 1 | 0 |
| **06** | Checkout Flow & Distance Conveyance | 12 | 7 | 5 | 0 | 0 |
| **07** | Customer Dashboard & Orders | 5 | 2 | 2 | 1 | 0 |
| **08** | Contact & Support Portal | 6 | 0 | 2 | 4 | 0 |
| **09** | Informational & Policy Pages | 3 | 0 | 0 | 2 | 1 |
| **10** | Cross-Browser & Mobile Usability | 4 | 0 | 3 | 1 | 0 |
| **11** | Security & Input Sanitization | 5 | 4 | 1 | 0 | 0 |
| **12** | SEO, Schema & Performance | 3 | 0 | 0 | 3 | 0 |
| **TOTAL** | **Comprehensive Test Suite** | **77** | **23** | **27** | **25** | **2** |

---

## 🛠️ Defect Reporting Template (Recommended Format)

When executing the above test cases, record any discovered defects using the following standard format:

```markdown
### 🐛 Bug Report: [Short Title]
- **Bug ID:** BUG-FXZ-XXX
- **Test Case ID:** [e.g. TC-CHK-005]
- **Severity:** [Critical / High / Medium / Low]
- **Environment:** Windows 11 / Chrome 128 / Mobile Safari iOS 17
- **Preconditions:** [User logged in with items in cart]
- **Steps to Reproduce:**
  1. Go to /services/ac-master-service
  2. Select 2 packages and click checkout
  3. Enter delivery address > 10 km
- **Actual Result:** [Conveyance fee shows ৳0 instead of calculating distance rate]
- **Expected Result:** [Conveyance fee should calculate base fee + (distance - 3km) * 15 BDT]
- **Screenshots / Logs:** [Attach screenshot / console logs]
```

---
*Document maintained by Fixzone QA Team. For updates or automated test scripts (Playwright / Cypress), contact `admin@fixzone.com.bd`.*
