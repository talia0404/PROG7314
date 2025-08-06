# ✅ **Step 2: Android App Setup **

---

### 🧱 1. **Create a New Android Project**

#### In Android Studio:Here’s a version of your **Step 2: Android App Setup** that uses **Kotlin-style Gradle syntax** (not Groovy) and follows proper formatting for `build.gradle.kts` files (i.e., when you're using Kotlin DSL in Android Studio):

---

## ✅ Step 2: Android App Setup (Kotlin DSL version)

---

### 🧱 1. **Create a New Android Project**

In Android Studio:

1. Click **New Project**
2. Choose **Empty Activity**
3. Name it: `MemeStreamApp`
4. Select **Kotlin**
5. Min SDK: **21 (Lollipop)**
6. Click **Finish**

---

### 🗂️ 2. **Recommended Folder Structure**

```
MemeStream/
└── MemeStreamApp/         ← Android app
    ├── app/
    └── build.gradle.kts
```

---

### ⚙️ 3. **Add Permissions**

In `src/main/AndroidManifest.xml`, above `<application>`, add:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

---

### ⚙️ 4. **Enable ViewBinding**

In your `build.gradle.kts (Module: app)`:

```kotlin
android {
    ...
    buildFeatures {
        viewBinding = true
    }
}
```

---

### 📦 5. **Add Dependencies** (in Kotlin DSL)

In `build.gradle.kts` (Module: `app`), update the `dependencies` block:

```kotlin
dependencies {
    // Retrofit + Moshi
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-moshi:2.9.0")
    implementation("com.squareup.moshi:moshi-kotlin:1.13.0")

    // Glide
    implementation("com.github.bumptech.glide:glide:4.12.0")
    kapt("com.github.bumptech.glide:compiler:4.12.0")

    // Google Maps + Location
    implementation("com.google.android.gms:play-services-maps:18.1.0")
    implementation("com.google.android.gms:play-services-location:21.0.1")

    // Twitter SDK (or use ACTION_SEND intent instead)
    implementation("com.twitter.sdk.android:twitter:3.3.0")

    // Biometric authentication
    implementation("androidx.biometric:biometric:1.1.0")

    // Room DB
    implementation("androidx.room:room-runtime:2.6.1")
    kapt("androidx.room:room-compiler:2.6.1")
    implementation("androidx.room:room-ktx:2.6.1")
}
```

And in the top of the same file:

```kotlin
plugins {
    id("com.android.application")
    kotlin("android")
    kotlin("kapt")
}
```

---

### 🔄 6. **Sync Gradle**

Click **“Sync Now”** in Android Studio (yellow bar). Resolve any sync errors.

---

### 🗺️ 7. **Google Maps API Key Setup**

1. Go to: [https://console.cloud.google.com](https://console.cloud.google.com)
2. Enable **Maps SDK for Android**
3. Generate an **API key**
4. In `AndroidManifest.xml`, inside `<application>`:

```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_GOOGLE_MAPS_API_KEY"/>
```

---

### 🔐 8. **Biometric Prompt Setup**

No extra setup needed — just use `BiometricPrompt` in your `LoginActivity`.

---

### 🧪 9. **Test the Project**

In `MainActivity.kt`, add:

```kotlin
Log.d("Startup", "✅ Project setup complete!")
```

---

### ✅ Final Checklist

| Item                                 | Status |
| ------------------------------------ | ------ |
| Android app created with Kotlin      | ✅      |
| Permissions added                    | ✅      |
| Dependencies (Retrofit, Moshi, etc.) | ✅      |
| Google Maps + Location               | ✅      |
| Room + Biometric                     | ✅      |
| Gradle synced successfully           | ✅      |

---

Let me know if you'd like the actual `build.gradle.kts` file scaffold or setup help for any specific feature next (e.g. Retrofit setup or Google Maps fragment).


1. Open Android Studio → `New Project`
2. Choose **Empty Activity**
3. Name your project: `MemeStreamApp`
4. Language: **Kotlin**
5. Minimum SDK: **API 21 (Lollipop)**
6. Finish → Android Studio generates your `MainActivity.kt` and `activity_main.xml`.

---

### 🗂️ 2. **Project Folder Structure**

Recommended top-level structure:

```
MemeStream/
├── 01-RestfulAPI/         ← your backend
└── MemeStreamApp/         ← your Android app
    ├── app/
    └── build.gradle
```

---

### ⚙️ 3. **Add Permissions**

Open `AndroidManifest.xml` inside `src/main/` and add these lines **above** the `<application>` tag:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

> ✅ Required for accessing APIs and user location.

---

### ⚙️ 4. **Enable ViewBinding (optional but helpful)**

In `build.gradle (Module: app)`:

```kotlin
android {
    ...
    buildFeatures {
        viewBinding = true
    }
}
```

---

### 📦 5. **Add Dependencies to `build.gradle (Module: app)`**

Open `MemeStreamApp/app/build.gradle` and add the following inside `dependencies { ... }`:

#### 🔹 Retrofit + Moshi

```kotlin
implementation ('com.squareup.retrofit2:retrofit:2.9.0')
implementation ('com.squareup.retrofit2:converter-moshi:2.9.0')
implementation ('com.squareup.moshi:moshi-kotlin:1.13.0')
```

#### 🔹 Glide (for GIF/image loading)

```kotlin
implementation ('com.github.bumptech.glide:glide:4.12.0')
kapt ('com.github.bumptech.glide:compiler:4.12.0')
```

Make sure you enable Kotlin annotation processing at the top of the file:

```kotlin
apply plugin: ('kotlin-kapt')
```

#### 🔹 Google Maps + Fused Location

```kotlin
implementation ('com.google.android.gms:play-services-maps:18.1.0')
implementation ('com.google.android.gms:play-services-location:21.0.1')
```

#### 🔹 Twitter Kit (or use share intent)

```kotlin
implementation ('com.twitter.sdk.android:twitter:3.3.0')
```

> Or skip this and use:

```kotlin
val intent = Intent(Intent.ACTION_SEND)
```

#### 🔹 Biometric Authentication

```kotlin
implementation ("androidx.biometric:biometric:1.1.0")
```

#### 🔹 RoomDB (for offline caching)

```kotlin
implementation ("androidx.room:room-runtime:2.6.1")
kapt ("androidx.room:room-compiler:2.6.1")
implementation ("androidx.room:room-ktx:2.6.1")
```

---

### 🔄 6. **Sync Gradle**

After updating dependencies, click **“Sync Now”** in the yellow bar in Android Studio.

---

### 🗺️ 7. **Configure Google Maps**

1. Go to: [https://console.cloud.google.com/](https://console.cloud.google.com/)
2. Create a project or select existing
3. Enable **Maps SDK for Android**
4. Generate **API Key**
5. In `AndroidManifest.xml`, inside `<application>`, add:

```xml
<meta-data
    android:name="com.google.android.geo.API_KEY"
    android:value="YOUR_GOOGLE_MAPS_API_KEY"/>
```

---

### 🔐 8. **Enable Biometric Prompt**

No special setup — just use `BiometricPrompt` in your login activity.

---

### 🧪 9. **Test Basic Functionality**

Add a `Log.d("API", "Project setup complete!")` in `MainActivity.kt` to confirm it compiles.

---

### ✅ Final Checks

| Item                                     | Status |
| ---------------------------------------- | ------ |
| App created (min SDK 21)                 | ✅      |
| Permissions added                        | ✅      |
| Libraries added (Retrofit, Moshi, Glide) | ✅      |
| Google Maps & Location SDK               | ✅      |
| Biometric & RoomDB added                 | ✅      |
| Gradle synced successfully               | ✅      |

---
