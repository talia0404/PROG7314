## 🧩 1. Clean and Prepare Your App

Before you even think of publishing:

* **Versioning:**
  Open your `build.gradle (Module: app)` file and set:

  ```gradle
  defaultConfig {
      applicationId "com.yourapp.name"
      versionCode 1
      versionName "1.0"
  }
  ```

  Each Play Store update requires a new `versionCode`.

* **Remove debug logs and print statements:**
  Replace any `Log.d()` or `println()` with production-safe logging (or remove them).

* **Turn off debugging:**
  In `AndroidManifest.xml`, make sure:

  ```xml
  android:debuggable="false"
  ```

* **App icon and assets:**
  Go to **app → res → mipmap** and replace all launcher icons with your final ones.
  You can use Android Studio’s **Image Asset Studio** to generate proper sizes.

---

## 🔐 2. Create a Signed APK or App Bundle

Play Store no longer accepts APKs - use **Android App Bundle (AAB)**.

### In Android Studio:

1. Click **Build > Generate Signed App Bundle / APK**.
2. Choose **Android App Bundle** → **Next**.
3. Create a new **keystore** (if you don’t have one):

   * Store Path: `keystore.jks`
   * Password: something safe (don’t lose this)
   * Key alias: `release`
   * Key password: same or new.
4. Select your key, click **Next** → **Release** build → **Finish**.

You’ll find your `.aab` file in:
`/app/release/app-release.aab`

---

## 🧹 3. Test Your Release Build

Before uploading:

* Install it manually on your phone:

  ```
  adb install app-release.aab
  ```

  or use Android Studio → **Build → Build Bundle(s) / APK(s)** → **Locate** → **Install**.
* Verify all key features:

  * SSO login works
  * API connects properly
  * App doesn’t crash on invalid inputs
  * Permissions requests behave properly

---

## 💼 4. Set Up Your Google Play Console

Go to [https://play.google.com/console](https://play.google.com/console)

1. Sign in with your **developer account** (or pay once-off $25 if new).
2. Click **Create app**.
3. Fill in:

   * **App name**
   * **Default language**
   * **App type:** App or Game
   * **Free or Paid**
   * Tick “I confirm” policies.

---

## 🧾 5. Complete Store Listing

In your new app dashboard:

* **App details:** Name, short & full description.
* **Graphics:**

  * App icon (512x512)
  * Feature graphic (1024x500)
  * Phone screenshots (2–8 required).
* **Categorisation:**

  * Type → App
  * Category → e.g. Productivity / Finance
  * Content rating → Fill in questionnaire.
* **Privacy Policy:**
  Add a hosted link (GitHub Pages, Render, or Firebase Hosting works fine).

---

## 🧰 6. Upload Your App Bundle (.aab)

Go to:
**Release → Production → Create new release**

* Upload your `.aab` file.
* Add release notes (changes since last version).
* Click **Save**, then **Review release**, then **Start rollout to production**.

---

## ✅ 7. Wait for Review

Google typically takes **1–3 days** for new apps.
If rejected, they’ll tell you what to fix - usually content rating, missing policy, or permissions justification.

---

## 🧩 Resources

- Publish your app,  https://developer.android.com/studio/publish
- Publishing overview, https://play.google.com/console/about/publishingoverview/
- How to Publish Your Android App on Google Play Store?, https://www.geeksforgeeks.org/android/how-to-publish-your-android-app-on-google-play-store/

---

