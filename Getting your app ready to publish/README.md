# 🚀 Deploying Your Android App to Google Play Store

Publishing your Android app is the final milestone before it reaches real users. Follow this guide step-by-step to ensure your app is polished, compliant, and production-ready.

---

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
   * Key password: same or new
4. Select your key → click **Next** → choose **Release** build → **Finish**.

You’ll find your `.aab` file in:

```
/app/release/app-release.aab
```

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

## 💼 4. Create a Google Play Developer Account

1. Go to the [Google Play Console](https://play.google.com/console) website and sign up.
2. Pay the **one-time registration fee** of **$25**.
3. Agree to the **Developer Distribution Agreement** and verify your identity.
4. Choose whether to create the account as an **individual** or for a **company**.

---

## 🧩 5. Prepare Your App

1. Finalize your app and generate a **signed APK or Android App Bundle (.aab)**.
2. Prepare all necessary information, including:

   * App name
   * Detailed description
   * Monetization strategy (if applicable)
3. If you plan to sell apps or offer in-app purchases, link your developer account to a **Google Merchant Account**.

---

## ⚙️ 6. Set Up Your App in the Play Console

1. Navigate to **All apps** and click **Create app**.
2. Specify:

   * App name
   * Default language
   * Type (App or Game)
   * Free or Paid
3. Complete the **App Content** section:

   * Add your **Privacy Policy**
   * Declare **ads usage**
   * Fill out the **Content Rating** questionnaire
   * Complete **Data Safety disclosure**
4. Configure **pricing and distribution** settings (countries, device types, etc.).

---

## 🧾 7. Prepare the Store Listing

In your new app dashboard:

* **App details:**

  * Name, short & full description.

* **Graphics:**

  * App icon (512×512 PNG)
  * Feature graphic (1024×500 JPG/PNG)
  * 2–8 screenshots (required for phone).

* **Categorisation:**

  * Type → App
  * Category → e.g., Productivity / Finance
  * Content rating → Complete questionnaire.

* **Privacy Policy:**
  Add a hosted link (GitHub Pages, Render, or Firebase Hosting works fine).

* **Tags:**
  Add relevant tags to improve discoverability.

---

## 🧪 8. Test and Release Your App

1. Upload your app bundle to a **test track** (e.g., internal or closed testing).
2. For **new personal accounts**, Google requires:

   * A **closed test** with at least **20 testers**,
   * A **minimum of 14 days** of testing **before** a production release.
3. After successful testing, you can:

   * Roll out to **production review**,
   * Then choose to release the app to **all users** or use a **staged rollout**.

---

## 🧰 9. Upload Your App Bundle (.aab)

Go to:
**Release → Production → Create new release**

* Upload your `.aab` file.
* Add **release notes** (changes since last version).
* Click **Save**, then **Review release**, then **Start rollout to production**.

---

## ✅ 10. Wait for Review

Google typically takes **1–3 days** to review new apps.
If rejected, check your Play Console email for the reason - usually related to:

* Content rating
* Missing privacy policy
* Permission misuse or policy violations

Once approved, your app will go live on the Play Store!

---

## 🧩 11. Useful Resources

* **Official Docs:** [Publish your app](https://developer.android.com/studio/publish)
* **Play Console Overview:** [Publishing overview](https://play.google.com/console/about/publishingoverview/)
* **Step-by-step Guide:** [GeeksforGeeks - How to Publish Your Android App](https://www.geeksforgeeks.org/android/how-to-publish-your-android-app-on-google-play-store/)

