# Fight Cafe — TestFlight & App Store Submission Checklist

Work through these in order. Each section maps to a specific part of App Store Connect or Xcode.

---

## Phase 1 — Pre-flight (do this before touching App Store Connect)

### Xcode project settings
- [ ] **Bundle ID** set to `com.yourname.fightcafe` (Xcode → Target → Signing & Capabilities → Bundle Identifier)
- [ ] **Version** set to `1.0.0` and **Build** set to `1` (Xcode → Target → General → Identity)
- [ ] **Deployment target** set to iOS 17.0 (minimum for SwiftData + UnevenRoundedRectangle)
- [ ] **Display name** is "Fight Cafe" (not "FightCafe")
- [ ] **Signing** is set to "Automatically manage signing" with your Apple Developer Team selected
- [ ] Scheme destination is **iPhone 16 Pro** (or any iOS simulator — NOT "My Mac")
- [ ] `⇧⌘K` Clean Build Folder → `⌘B` Build → **0 errors, 0 warnings** (fix all warnings too)

### Capabilities
- [ ] **Sign in with Apple** capability is ON (Xcode → Signing & Capabilities → + Capability)
- [ ] **CoreLocation** — Privacy strings added to `Info.plist`:
  ```
  NSLocationWhenInUseUsageDescription
  → "Fight Cafe uses your location to show nearby gyms and open mats."
  ```
- [ ] No other sensitive capabilities requested without usage strings

### Legal site live
- [ ] `https://fightcafe.app/privacy` returns 200 in Safari
- [ ] `https://fightcafe.app/terms` returns 200 in Safari
- [ ] Email forwarding active: `privacy@fightcafe.app` and `hello@fightcafe.app`

---

## Phase 2 — App Icons & Screenshots

### App icon
- [ ] 1024×1024 px PNG, no alpha channel, no rounded corners (Apple adds them)
- [ ] Added to `Assets.xcassets → AppIcon` in Xcode
- [ ] Suggested design: dark purple gradient background + white 🥋 figure.martial.arts SF Symbol

### Screenshots (required per device class)
Upload at least 2 sizes. Minimum: iPhone 6.9" + iPhone 6.5".

| Device           | Resolution      |
|------------------|-----------------|
| iPhone 6.9"      | 1320 × 2868 px  |
| iPhone 6.5"      | 1284 × 2778 px  |
| iPad Pro 13"     | 2064 × 2752 px  *(optional but recommended)* |

**5 suggested screens to capture (on simulator):**
1. Dashboard — streak card + weekly load chart
2. Map — gym pins + selected gym card
3. Training Log — session list
4. Profile — belt progress + Mat Passport
5. Journal — latest note card

> Use **Xcode → Simulator → File → Take Screenshot** or `⌘S` in Simulator.  
> Polish in Figma/Canva with a device frame and short caption.

---

## Phase 3 — TestFlight Internal Testing

1. **Archive the build**:  
   Xcode → Product → Archive (scheme must be set to **Any iOS Device (arm64)**)
2. **Distribute**:  
   Organizer → Distribute App → App Store Connect → Upload
3. **Wait for processing** (~10–20 min; Apple runs automated checks)
4. In App Store Connect → TestFlight → Internal Testing:
   - Add yourself + up to 24 others (no review needed for internal)
   - Install via TestFlight app on a real device
5. **Smoke-test on device** (real hardware behaves differently from simulator):
   - [ ] Sign in with Apple works end-to-end
   - [ ] Location permission prompt appears
   - [ ] Map loads with gym pins
   - [ ] Log session → session appears in Training Log
   - [ ] Journal entry saves and persists after app restart
   - [ ] Sign out → sign back in → data restored
   - [ ] App doesn't crash on cold launch

### External TestFlight (optional, before App Store)
- Requires 1–3 day Beta App Review
- Up to 10,000 testers via public link
- Add a "What to test" description in App Store Connect

---

## Phase 4 — App Store Connect Setup

### Create the app record (if not already done)
App Store Connect → Apps → **+** → New App  
- Platform: iOS  
- Name: **Fight Cafe**  
- Primary Language: English (U.S.)  
- Bundle ID: select `com.yourname.fightcafe`  
- SKU: `fightcafe-ios-v1` (internal reference, never shown publicly)

### App Information tab
- [ ] Subtitle: `BJJ Training Tracker` (30 chars max)
- [ ] Category: **Sports** / Sub-category: **Health & Fitness**
- [ ] Content Rights: "This app does not contain, show, or access third-party content"
- [ ] Age Rating: complete the questionnaire (likely 4+)

### Pricing & Availability
- [ ] Price: **Free** (or set your tier)
- [ ] Availability: all territories (or restrict as needed)
- [ ] Pre-order: not needed for v1

### App Privacy (Nutrition Label)
Fill out the Data Types questionnaire honestly — it must match your Privacy Policy.

| Data type         | Collected? | Linked to user? | Used for tracking? |
|-------------------|------------|-----------------|-------------------|
| Name              | Yes        | Yes             | No                |
| Email address     | No         | —               | —                 |
| User ID           | Yes        | Yes             | No                |
| Coarse location   | Yes        | No              | No                |
| Other user content (journal) | Yes | Yes          | No                |
| Crash data        | Yes        | No              | No                |

### Version Information (Prepare for Submission)
- [ ] **App name**: Fight Cafe
- [ ] **Description** (4000 chars max):
  ```
  Fight Cafe is the training companion built for BJJ practitioners who 
  want to track their progress, discover open mats, and own their journey 
  on the mats.

  FEATURES
  • Session Logging — track duration, techniques, and intensity for every roll
  • Streak Tracker — stay accountable with daily streaks and milestone rewards
  • Weekly Load Chart — visualise your training volume across the week
  • Open Mat Map — find gyms hosting open mats tonight with Gi/No-Gi filters
  • Mat Passport — collect a stamp for every gym you visit; rate on Google Maps
  • Training Journal — write post-session notes to reinforce what you learned
  • Belt Progress — track stripes and see your path to the next rank

  Built for white belts grinding their first year and black belts still 
  hunting submissions.
  ```
- [ ] **Keywords** (100 chars max, comma-separated):  
  `bjj,jiu jitsu,grappling,training log,martial arts,open mat,streak,belt tracker`
- [ ] **Promotional text** (170 chars, updateable without re-review):  
  `Now with Open Mat Map — find gyms near you hosting open mats tonight.`
- [ ] **Support URL**: `https://fightcafe.app`
- [ ] **Marketing URL**: `https://fightcafe.app`
- [ ] **Privacy Policy URL**: `https://fightcafe.app/privacy`

### Sign in with Apple note
Because you use Sign in with Apple, your app **requires** an account deletion flow.  
Verify: Profile → Account → "Delete Account" button exists and works. ✓ (already built)

---

## Phase 5 — Submit for Review

1. In the Prepare for Submission page, select your TestFlight build
2. Answer the Export Compliance questionnaire:
   - "Does your app use encryption?" → **Yes** (HTTPS/TLS)
   - "Is it exempt?" → **Yes** (standard HTTPS — check "This app uses only exempt encryption")
3. Answer the Advertising Identifier (IDFA) question → **No** (we don't use IDFA)
4. Click **Submit for Review**

### Review timeline
- First submission: typically **24–48 hours**
- Expedited review available if you have a critical launch date (request via Resolution Center)

---

## Phase 6 — Post-Approval

- [ ] Set release to **Manual Release** so you control the exact launch moment
- [ ] OR set a **Scheduled Release** date
- [ ] After approval, click **Release This Version**
- [ ] Update `index.html` App Store button with the real `https://apps.apple.com/app/id...` link
- [ ] Post on social / notify beta testers
- [ ] Monitor **Crashes** tab in App Store Connect for the first 48 hrs

---

## Common Rejection Reasons to Pre-empt

| Reason | Prevention |
|---|---|
| Missing privacy policy URL | Already handled — `fightcafe.app/privacy` |
| Account deletion not working | Built in Profile → Account → Delete Account |
| Sign in with Apple missing | Added as a capability + fully implemented |
| Guideline 5.1.1 — data collection | Privacy nutrition label matches policy |
| Location usage string missing | Add `NSLocationWhenInUseUsageDescription` to Info.plist |
| Screenshots don't match app | Capture from real build, not mockups |
| Binary contains non-public API | Run `⌘B` on Release scheme, check for warnings |

---

## Quick Reference

| Item | Value |
|---|---|
| App name | Fight Cafe |
| Bundle ID | com.yourname.fightcafe |
| Version | 1.0.0 |
| Min iOS | 17.0 |
| Category | Sports |
| Privacy URL | https://fightcafe.app/privacy |
| Support URL | https://fightcafe.app |
| Export compliance | Exempt (standard HTTPS only) |
| IDFA | No |
