# 🌍 TranslatorApp — Student Instructions

We’re building a **super simple Android translator app** using **XML Views** (no Jetpack Compose, no deprecated APIs). The app will let users:

1. ✍️ Type text in one language.
2. 🔄 Pick a “from” language and a “to” language.
3. 🌐 See the translated text appear on screen.

---

## 🛠️ Step 1 — Project Setup

1. Open **Android Studio**.
2. Create a new project → choose **Empty Views Activity**.
3. Set the package name: `com.talia.translatorapp`.
4. Use **Kotlin** and minimum SDK **21 or higher**.

---

## 📦 Step 2 — Add Dependencies

1. Open `build.gradle (app level)`.
2. Add:

   * **AppCompat / Material / ConstraintLayout** → for UI.
   * **ML Kit Translate** → this handles on-device translations.
3. Sync Gradle after editing.

---

## 🗂️ Step 3 — Layout Design (XML)

1. Add an **EditText** so the user can type text.
2. Add **two Spinners** → one for the source language, one for the target.
3. Add a **Button** → “Translate”.
4. Add a **TextView** → where the translated text will appear.
5. Add a **ProgressBar** → to show while translation is working.

---

## ⚡ Step 4 — Language Setup

1. Create a **list of languages** (e.g., English, Spanish, French, German).
2. Attach them to the **spinners** so the user can select.
3. Default: From = English 🇬🇧 → To = Spanish 🇪🇸.

---

## 🔧 Step 5 — Translation Logic

1. When the **Translate button** is clicked:

   * Get the input text.
   * Check which languages are chosen in the spinners.
   * If they’re the same → just show the same text.
   * Otherwise → use **ML Kit** to download the translation model (only once per language) and translate.
2. Show the translated text in the TextView.
3. If something fails (e.g., no internet for the first download) → show a Toast message.

---

Resources: 
- https://developer.android.com/training/basics/supporting-devices/languages
- https://medium.com/@khush.panchal123/supporting-multiple-languages-in-your-android-application-a08e21b1baf1


