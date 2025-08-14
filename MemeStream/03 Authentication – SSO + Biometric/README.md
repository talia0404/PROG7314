# ✅ Step 3: Authentication – Overview

| Requirement                | Explanation                                           |
| -------------------------- | ----------------------------------------------------- |
| ✅ Firebase Authentication  | For **SSO (Google Sign-In)**                          |
| ✅ Biometric Authentication | For **fingerprint/face login** (on supported devices) |

You'll implement:

* **SSO using Google Sign-In** via Firebase
* **BiometricPrompt** for local device authentication

---

### 🧱 Tools Used

* Firebase Authentication
* Google Sign-In
* AndroidX Biometric API

---

## 📦 Step 1: Add Dependencies (Kotlin DSL)

In your `build.gradle.kts` (**Kotlin DSL**) file for your app module (`MemeStreamApp/app/build.gradle.kts`), add the following:

```kotlin
dependencies {
    // Firebase BoM – keeps Firebase versions in sync
    implementation(platform("com.google.firebase:firebase-bom:32.7.0"))

    // Firebase Auth
    implementation("com.google.firebase:firebase-auth-ktx")

    // Google Sign-In
    implementation("com.google.android.gms:play-services-auth:20.7.0")

    // Biometric Authentication
    implementation("androidx.biometric:biometric:1.1.0")
}
```

In your build gradle project level, **apply the Firebase plugin** if you haven’t already:

```kotlin
plugins {
        id("com.google.gms.google-services") version "4.4.2" apply false
}
```

In your **project-level** `build.gradle.kts` file:

```kotlin
plugins {
    id("com.google.gms.google-services")
}
```

Then sync Gradle.

---

## 🔥 Step 2: Set Up Firebase in the Project

1. Go to [https://console.firebase.google.com](https://console.firebase.google.com)
2. Create a project (e.g., `MemeStream`)
3. Add Android app:

   * Package name: Must match your Android app
   * Download the `google-services.json` file and place it in:

     ```
     MemeStreamApp/app/google-services.json
     ```
4. Back in Firebase Console:

   * Enable **Authentication**
   * Enable **Google Sign-In provider**

---

## 🧭 Step 3: Plan Your Implementation 

### 🔐 Part A: Google Sign-In with Firebase

### ✅ 1. Prerequisites Recap

Before starting:

* Firebase project is set up ✅
* `google-services.json` is placed in `app/` ✅
* Firebase Auth and Google Sign-In are enabled ✅
* All dependencies in Kotlin DSL are added ✅

### 🧩 2. AndroidManifest Setup

In your `AndroidManifest.xml`, add:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

Inside `<application>`, add:

```xml
<meta-data
    android:name="com.google.android.gms.version"
    android:value="@integer/google_play_services_version" />
```

### 🔧 3. Set up Google Sign-In in Your App

#### a. **Create a LoginActivity or Fragment**

This screen will:

* Display a “Sign in with Google” button
* Handle Firebase Auth

#### b. **In LoginActivity.kt** 

1. **Initialize FirebaseAuth**

   * `FirebaseAuth.getInstance()`

2. **Configure Google Sign-In Options**

   * Request the user’s ID token and email
   * Use `GoogleSignInOptions.Builder`

3. **Create a `GoogleSignInClient`**

   * This launches the Google sign-in screen

4. **Launch sign-in Intent on button click**

   * Use `signInIntent = googleSignInClient.signInIntent`

5. **Handle result in `onActivityResult()` or `ActivityResultLauncher`**

   * Get the `GoogleSignInAccount` from the result
   * Extract the ID token

6. **Send the token to Firebase**

   * Call `signInWithCredential()` using a `GoogleAuthProvider.credential(idToken)`

7. **On success, navigate to the main app (and trigger biometric)**


#### **Resources:**

Authenticate with Google on Android:   
https://firebase.google.com/docs/auth/android/google-signin

---

### ✅ Part B: Biometric Authentication

**Resources:**

Implement Biometric Authentication in Android Apps:   
https://pranaypatel.medium.com/implement-biometric-authentication-in-android-apps-f091fbbb9988

BiometricPrompt protects local access to that already-signed-in session on this device.

Think of it like: “You’re signed in as XYZ via Google—now prove it’s you before we show data."

### 🧩 1. Where to Place Biometric Flow

After first successful Google sign-in: ask the user to enable biometrics.

On subsequent app launches (if FirebaseAuth.getCurrentUser() ≠ null and user enabled biometrics): gate entry with BiometricPrompt.

If biometric fails or hardware/enrollment is missing, fall back to normal sign-in.

You can place biometric login:

* **Immediately after Google sign-in**, OR
* **At app launch** if user is already authenticated

### ⚙️ 2. Prerequisites & Setup

#### a. Check availability:

* Ensure device has biometric hardware
* Check that a fingerprint or face is enrolled

#### b. Set up `BiometricPrompt`

The biometric system needs:

* `BiometricPrompt`
* `PromptInfo` (the UI config)

### 🧠 3. Your Flow 

1. **Create a helper class or reuse LoginActivity**

2. When app starts or user logs in:

   * Show `BiometricPrompt`
   * Provide success and failure callbacks

3. On success:

   * Navigate to main screen (e.g., `MainActivity`)

4. On failure:

   * Show error and optionally allow retry

---

### 💡 Notes

* Firebase handles secure user login + SSO
* BiometricPrompt protects access to local data or sessions
* You can store biometric preference using `SharedPreferences`

---

## 🎯 Suggested Authentication Flow

```plaintext
[Launch App]
   ↓
[Check Firebase Auth state]
   ↓
[Not logged in? → Show Google Sign-In]
   ↓
[On successful sign-in → Trigger BiometricPrompt]
   ↓
[On biometric success → Enter App]
```

---
