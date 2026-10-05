# Playrix QA & UX Case Study: Homescapes
**Candidate:** Oksana Nekritova  
**Target Role:** Junior QA Engineer  
**Product Analyzed:** Homescapes (Android)  

---

## 1. UX & Usability Analysis

> *Product and UX observations gathered during exploratory testing on Android devices.*

* **Language Selector Native Endonym Fallback:**  
  When switching to **Simplified Chinese** or **Traditional Chinese**, all other language names in the selector modal switch to Chinese ideograms (e.g., *English* becomes *英文*). If a non-Chinese player accidentally selects this language, they lose the ability to navigate back. Language names in selectors should always retain their native script (Endonyms).
*Attachment:* 🎬 [Watch Video: Language Selector Bug] https://github.com/user-attachments/assets/f4fa00a1-c1e8-421d-bfe8-3554714a5fff

*Attachment:* 🎬 [Watch Video: Language Selector Bug](l10n_language_bug.mp4)
* **Non-Interactive Event Energy Counter (`5/1000` Toolbar):**  
  Tapping the blue energy indicator (`5/1000`) on the top bar yields no UI response or informational tooltip. For new players (FTUE), this lacks clarity—adding an explanatory pop-up on tap would improve usability.
  *Attachment:* 🎬 [Watch Video: Energy Counter UI Issue](energy_toolbar_ux.mp4)
* **Confusing Account Linking Text ("Save Progress" Modal):**  
  In the settings overlay, under *"Connect to save progress"*, the action buttons display *"Log out of Facebook"* / *"Log out of Google"* when already connected. The call-to-action contradicts the dialog header, confusing users trying to verify their progress save status.
  *Attachment:* 📸 [Screenshot: Progress Save Modal Logic Contradiction](save_progress_modal.jpg)
* **Unresponsive UI / Input Lag on Mini-Game "Play" Button:**  
  Tapping the *"Play"* button (with the exclamation badge) in the Mini-Games menu requires multiple consecutive taps before triggering the level load scene. The lack of an immediate visual pressed-state or loading indicator leads to user frustration.
  *Attachment:* 🎬 [Watch Video: Play Button Input Lag](minigame_play_button_lag.mp4)

---

## 2. Test Documentation Examples

### A. Test Cases

| Test Case ID | Feature / Component | Preconditions | Test Steps | Expected Result | Status |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-001** | Interruptions: Incoming Phone Call | Game session active during Match-3 level. | 1. Trigger an incoming cellular call.<br>2. Accept call and speak for 10s.<br>3. End call and return to game. | Game automatically pauses; upon return, board state and level progress are restored without data loss. | **PASSED** |
| **TC-002** | Interruption / Recovery: Battery Depletion Shutdown | Active gameplay session; low battery state. | 1. Allow mobile battery to drain until system power-off.<br>2. Recharge and relaunch app. | Application restores game state to the last server sync checkpoint without corrupted save data. | **PASSED** |
| **TC-003** | Localization: Language Selector Consistency | Access Settings -> Language Selection menu. | 1. Select *Traditional Chinese*.<br>2. Inspect remaining language button labels. | All unselected languages retain their native endonyms (e.g., *English*, *Русский*) to allow easy recovery. | **FAILED** *(See Bug Report)* |

---

### B. Bug Reports

#### Bug Report 1: Language menu breaks endonym display upon selecting Chinese languages
* **Severity:** Major  
* **Priority:** Medium  
* **Category:** Localization (L10n) / Usability (UX)  
* **Environment:** Android 9 / Samsung Galaxy / App Version 9.1.700  
* **Steps to Reproduce:**
  1. Open Game Settings -> Tap **Change Language**.
  2. Select **Traditional Chinese** (繁體中文) or **Simplified Chinese** (中文).
  3. Inspect the labels of other language options in the modal.
* **Expected Result:** Language names remain displayed in their native endonyms (e.g., *English*, *Deutsch*, *Русский*).
* **Actual Result:** All language names are translated into Chinese ideograms (e.g., *English* -> *英文*), making language recovery difficult for non-native speakers.
* *Attachments:* 🎬 [Video Recording: Chinese Language Selection Glitch](l10n_language_bug.mp4)

#### Bug Report 2: Contradictory button labeling in "Save Progress" settings modal
* **Severity:** Minor  
* **Priority:** Medium  
* **Category:** UX / Text Localization  
* **Environment:** Android 9 / Samsung Galaxy / App Version 9.1.700  
* **Steps to Reproduce:**
  1. Ensure the game account is already connected to Google / Facebook.
  2. Open Game Settings -> Tap **Save Progress**.
  3. Inspect the modal header, descriptive text, and action buttons.
* **Expected Result:**  
  * If connected: Header/Status displays *"Progress Saved"* or *"You are connected"* with dynamic status indicators (e.g., *"Connected"* or *"Disconnect"*).  
  * If NOT connected: Header displays *"Connect to save progress"* with action buttons prompts like *"Connect with Facebook"* / *"Connect with Google"*.
* **Actual Result:** Header displays *"Connect to save progress"*, while the action buttons say *"Log out of Facebook"* / *"Log out of Google"*, creating a logical contradiction for an already-connected account.
* *Attachment:* 📸 [Screenshot: Progress Save Modal Logic Contradiction](save_progress_modal.jpg)

---

## 3. QA Stack & Competencies
* **Testing Scope:** Manual Mobile Testing (Android), Interruption & Recovery Testing, Localization (L10n) & Usability (UX) Testing
* **Test Design Techniques:** Equivalence Partitioning (EP), Boundary Value Analysis (BVA), Decision Table Testing, State Transition Testing, Pairwise Testing, Error Guessing, Exploratory Testing.
* **Technical Tools:** Postman, Charles Proxy, Android Studio (Logcat), SQL, Jira, Confluence.
* **Animation & Narrative Background:** Screenwriting, storyboarding, script editing, 2D/3D animation pipelines, character motion timing, and visual QA (clipping, frame rates, texture artifacts).
