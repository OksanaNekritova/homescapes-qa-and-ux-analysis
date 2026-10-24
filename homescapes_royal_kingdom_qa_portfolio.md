# 🎮 Mobile Games QA & UX Case Study: Homescapes & Royal Kingdom

## 📌 Overview
This repository contains a comprehensive QA documentation and UX evaluation portfolio for mobile casual titles (**Homescapes** by Playrix and **Royal Kingdom** by Dream Games). 

The case study demonstrates practical software testing methodologies including **Functional Testing, Localization (L10n) Testing, Interruption Handling, Boundary Testing, and UX Flow Analysis** on real mobile devices.

---

## 📱 Test Environment
* **Device:** Samsung Galaxy S8
* **OS:** Android 9 (One UI 1.0)
* **Tested Applications:**
  * **Homescapes:** Version `9.2.102`
  * **Royal Kingdom:** Version `33931`

---

## 📝 Document Index

1. [Homescapes: Bug Reports](#-homescapes-bug-reports)
2. [Homescapes: UX & Flow Issues](#-homescapes-ux--flow-issues)
3. [Royal Kingdom: Bug Reports](#-royal-kingdom-bug-reports)
4. [Royal Kingdom: UX & Flow Issues](#-royal-kingdom-ux--flow-issues)

---

## 🐞 Homescapes: Bug Reports

### [BUG-01] Logical Contradiction in Progress Save Modal Dialog Text
* **Type:** Text Localization / UX Logic
* **Priority:** Medium | **Severity:** Minor
* **Location:** Settings Menu -> Save Progress Modal
* **Description:** When the user account is already linked to Google or Facebook, the modal header incorrectly states *"Connect to save progress"* ("Подключите для сохранения прогресса"), while the action buttons below offer to logout (*"Disconnect Facebook"* / *"Disconnect Google"*).
* **Preconditions:** Homescapes launched; logged into an authorized Google/Facebook account.
* **Steps to Reproduce:**
  1. From the main screen, tap Settings (Gear icon) -> Tap **Save Progress**.
  2. Inspect the modal window header, body text, and action buttons.
* **Expected Result:** If connected, the header should display confirmation (*"Progress Saved"* / *"You are connected"*).
* **Actual Result:** Direct contradiction between the header prompt (asking to connect) and button functionality (offering to logout/disconnect).
* **Proof:** [Video Recording](https://drive.google.com/file/d/1SiuBxkMn2ZHM9mfhinh7iyNdZkUnE09c/view?usp=drive_link)

---

### [BUG-02] Endonym Display Corruption in Language Selection Menu
* **Type:** Localization (L10n) / Usability (UX)
* **Priority:** Medium | **Severity:** Major
* **Location:** Settings Menu -> Language Selector
* **Description:** When switching the interface language to Traditional or Simplified Chinese, all other native language names in the list are translated into Chinese characters (e.g., *English* becomes *英文*). If selected accidentally, non-Chinese players cannot identify their native language to revert changes.
* **Steps to Reproduce:**
  1. Open Settings -> Tap **Change Language**.
  2. Select **Traditional Chinese (繁體中文)** or **Simplified Chinese (中文)**.
  3. Inspect the remaining options in the language selector.
* **Expected Result:** Language titles should always display in their native endonyms (e.g., *English*, *Deutsch*, *Русский*).
* **Actual Result:** All language titles convert to Chinese ideograms, blocking language recovery for non-native speakers.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1Rho99b1sTC1iC9oHy9kSq8PTBwlrQEEg/view?usp=sharing)

---

### [BUG-03] Non-Responsive "Tap to Skip" Control on Post-Match Victory Screen
* **Type:** UI / Non-Responsive Control
* **Priority:** Medium | **Severity:** Minor
* **Location:** Match-3 Level Completion -> Victory Celebration Animation
* **Description:** The "Tap to Skip" prompt on the victory fireworks screen fails to accept touch input events, forcing players to wait through unskippable non-interactive animations.
* **Steps to Reproduce:**
  1. Complete any Match-3 level.
  2. Tap the screen or "Tap to Skip" button during the fireworks animation.
* **Expected Result:** Tapping should immediately skip or speed up the victory animation and proceed to reward calculation.
* **Actual Result:** Screen taps are ignored, forcing the player to wait for the entire animation timeline.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1-8Rqa9R0Z-QL9M2QAbY7CfNkIuPxauFB/view?usp=sharing)

---

## 🎨 Homescapes: UX & Flow Issues

### [UX-01] Unclear User Journey: "Rate Now" Redirects to Generic Facebook Feed
* **Type:** UX / Flow Issue
* **Priority:** Medium | **Severity:** Minor
* **Location:** "Rate us on Facebook" Modal Window
* **Description:** Tapping "Rate now" opens the generic Facebook group wall instead of a direct deep link to the specific voting post or survey, creating high user drop-off.
* **Recommendation:** Configure deep links leading directly to the interactive poll/post, or rename the CTA to *"Visit Community"*.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1wnSRAK_SqRhsk4p2gAIf6unRf29UwbAn/view?usp=sharing)

---

### [UX-02] Unhandled Interruption: Missing Automatic Pause on OS System Notifications
* **Type:** Interruption Handling / UX Risk
* **Priority:** Low | **Severity:** Minor
* **Location:** Active Match-3 Gameplay
* **Description:** When low battery notifications (15% battery banner) pop up, the game does not trigger focus loss (`onPause`), overlaying key upper game grid tiles and risking misclicks or lost moves.
* **Recommendation:** Implement an `onWindowFocusChanged` handler to trigger automatic game pause when OS system banners appear.
* **Proof:** [Video Recording](https://drive.google.com/file/d/121c_iq4hpgGvsNLc71O7vYOZWfVqsZ91/view?usp=sharing)

---

### [UX-03] Non-Interactive Energy Counter Visual Cue
* **Type:** FTUE / UI Feedback
* **Priority:** Low | **Severity:** Minor
* **Location:** Top HUD (Energy Counter 5/1000)
* **Description:** Tapping the energy icon produces no response or tooltip, leaving new players unaware of how or where energy regenerates.
* **Recommendation:** Add a standard informational tooltip on touch.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1e_0LDQEwsRJXNh43amcX1RQK38WvV7Ze/view?usp=sharing)

---

### [UX-04] Input Latency and Visual Feedback Delay in Mini-Games Menu
* **Type:** UI Response Delay / UX
* **Priority:** Low | **Severity:** Minor
* **Location:** Mini-Games Menu -> "Play" Button
* **Description:** Tapping "Play" requires multiple consecutive taps before triggering level load, causing users to believe the application is unresponsive.
* **Recommendation:** Add an immediate tap animation and loading spinner upon first interaction.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1smwaDBHIyaAlAgGP4y9pXAzoUv1vaVZT/view?usp=sharing)

---

## 👑 Royal Kingdom: Bug Reports

### [BUG-RK01] Unescapable Redirect Loop & Session Reset during Video Ad Interaction
* **Type:** Functional / Ad Integration Issue
* **Priority:** High | **Severity:** Major
* **Location:** Post-Match Level Loss Screen (+5 Extra Moves via Video Ad)
* **Description:** Interacting with ad banners during rewarded video views forces redirection to Google Play. Attempting to return via the OS Back button causes session resets, infinite loading loops, or ad re-triggering, losing player level progress.
* **Steps to Reproduce:**
  1. Reach "0 moves left" in a Match-3 level.
  2. Select "Watch Ad for +5 Moves".
  3. Tap the ad banner to trigger Google Play redirect.
  4. Use OS navigation to return to the game.
* **Expected Result:** Game session restores cleanly to the level screen or reward distribution.
* **Actual Result:** Game enters a loading loop or resets session state, preventing level resumption.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1wcSVdZvDMJymoVVQ74k7rfZMo6WTxSMY/view?usp=sharing)

---

## 👑 Royal Kingdom: UX & Flow Issues

### [UX-RK01] Missing "Tap to Skip" Mechanics on Victory Banners
* **Type:** Flow / Interruption Issue
* **Priority:** Medium | **Severity:** Minor
* **Location:** Level Victory Screen
* **Description:** Full-screen victory animations played at level completion cannot be skipped by tapping, causing unnecessary idle delay between core gameplay loops.
* **Recommendation:** Implement instant animation skip on screen tap.
* **Proof:** [Video Recording](https://drive.google.com/file/d/1_48N8qygEQn8Wb9ximuVTb5yreHkDHjw/view?usp=sharing)