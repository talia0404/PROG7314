## 🧱 MemeStream App – Step-by-Step Build Plan

---

### ✅ **Step 1: Create Your Own RESTful API (as per POE)**

#### 🔧 Stack Suggestion: Node.js + Express + MongoDB Atlas

1. **Create a backend folder in your project** (`/MemeStream/01-RestfulAPI`)
2. Set up Express server:

   ```bash
   npm init -y
   npm install express mongoose cors dotenv
   ```
3. Build API with endpoints:

   * `POST /memes` – saves meme data
   * `GET /memes` – fetches all memes
   * `GET /memes?userId=...` – fetches memes by user
4. Connect to MongoDB Atlas or local MongoDB
5. Test with Postman
6. Host using Render, Railway, or Firebase Cloud Functions
7. ✅ **Now you meet the “Create and host your own API connected to a database” requirement**

---

### ✅ **Step 2: Android App Setup**

#### 🛠 Tools:

* Kotlin
* Min SDK 21
* Libraries: Retrofit, Moshi, Glide, Maps SDK, Twitter SDK, Biometric, RoomDB

1. Create a new Android project (`/MemeStreamApp`)
2. Update your `build.gradle`:

   * Add dependencies for:

     * `Retrofit + Moshi`
     * `Glide`
     * `Google Maps + Location`
     * `Biometric`, `Twitter SDK` (or use `Intent.ACTION_SEND`)
     * `RoomDB` (for offline + sync)
3. Add required permissions:

   ```xml
   <uses-permission android:name="android.permission.INTERNET"/>
   <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
   ```

---

### ✅ **Step 3: Authentication**

Implement **SSO login + biometric authentication**

* Use **Firebase Authentication** or **OAuth with Google**
* Add **BiometricPrompt** for fingerprint/face login (required in final PoE)

---

### ✅ **Step 4: Fragment UI Design**

Use one `MainActivity` with `BottomNavigationView` or `NavHostFragment`.

#### 🔹 `FeedFragment` – Trending Memes

* Use Retrofit to call GIPHY API
* Parse JSON with Moshi
* Show memes in RecyclerView with Glide

#### 🔹 `CreateMemeFragment` – Upload Meme

* Upload meme or select from device/GIPHY
* Add text overlay with PhotoEditor or Canvas
* Get current location using `FusedLocationProviderClient`
* Create JSON `{ userId, imageUrl, caption, lat, lng, timestamp }`
* POST to your API

#### 🔹 `MapFragment` – View Memes on Map

* Use `GoogleMap` + markers
* Fetch memes from your API
* Display locations with `LatLng` markers

#### 🔹 `ProfileFragment` – User’s Memes + Sharing

* Call your API: `GET /memes?userId=...`
* RecyclerView with share button
* Share via Twitter SDK or `Intent.ACTION_SEND`

---

### ✅ **Step 5: Offline Mode + RoomDB (Final PoE)**

* Use `RoomDB` to cache memes locally
* Sync to server when online
* Add background worker using `WorkManager` if needed

---

### ✅ **Step 6: Real-Time Notifications (Final PoE)**

* Use Firebase Cloud Messaging (FCM)
* Notify users when a new meme is posted nearby, or if a meme is trending

---

### ✅ **Step 7: Multi-language Support (Final PoE)**

* Add strings.xml for `values-af/`, `values-zu/`, etc.
* Switch based on system locale or app setting

---

### ✅ **Step 8: GitHub Integration + Testing**

* Commit often with messages
* Add README with:

  * App overview
  * Video link
  * API link
* Use **GitHub Actions** to automate builds:

  * YAML config: `/.github/workflows/build.yml`
* Add **unit tests** for ViewModels, Repos, etc.

---

### ✅ **Step 9: Final Touches for Play Store**

* Prepare icons and screenshots
* Sign APK or AAB
* Show upload preview to Play Console
* Add Release Notes in README

---

### ✅ Summary of Key Requirements Satisfied

| POE Requirement                   | Covered In        |
| --------------------------------- | ----------------- |
| ✅ Custom REST API connected to DB | Step 1            |
| ✅ JSON read/write using Moshi     | Step 4, Retrofit  |
| ✅ External APIs (GIPHY)           | FeedFragment      |
| ✅ Location and Google Maps        | MapFragment       |
| ✅ Biometric Authentication        | Login screen      |
| ✅ Offline mode + sync             | RoomDB (PoE)      |
| ✅ Push notifications              | FCM (PoE)         |
| ✅ Multi-language                  | strings.xml (PoE) |
| ✅ GitHub + Actions                | GitHub setup      |
| ✅ App ready for Play Store        | Final build       |

