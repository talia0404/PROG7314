# ✅ Step 2: Android App Setup 

---

### 🧱 1. **Create a New Android Project**

#### In Android Studio:

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
