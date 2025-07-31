# ✅ Step 4: Fragment UI Design – Full Guide

You will use:

* A **single `MainActivity.kt`**
* A **`BottomNavigationView`** or `NavHostFragment` with Navigation Component
* **4 Fragments**:

  * `FeedFragment`
  * `CreateMemeFragment`
  * `MapFragment`
  * `ProfileFragment`

---

## 📱 Step 1: Scaffold Navigation

### ✅ a. Setup Navigation Graph 

1. Add Navigation Component dependency:

   ```kotlin
   implementation("androidx.navigation:navigation-fragment-ktx:2.7.6")
   implementation("androidx.navigation:navigation-ui-ktx:2.7.6")
   ```

2. Create `res/navigation/nav_graph.xml` using the visual editor.

3. Add destinations for:

   * `FeedFragment`
   * `CreateMemeFragment`
   * `MapFragment`
   * `ProfileFragment`

4. Add a `BottomNavigationView` to `activity_main.xml`, along with a `FragmentContainerView` tied to `nav_graph`.

---

## 🔹 `FeedFragment` – Trending Memes

### 🎯 Features:

* Uses Retrofit to fetch memes from **GIPHY API**
* Parses JSON using **Moshi**
* Displays memes in a **RecyclerView** with **Glide**

### 🧩 Implementation Steps:

1. Create layout: `fragment_feed.xml`

   * Add `RecyclerView`
2. Create `FeedFragment.kt`
3. Define `GiphyService` Retrofit interface
4. Use `ViewModel` + `LiveData` for clean architecture
5. Create `GiphyResponse` data classes for Moshi
6. Load data in ViewModel using Retrofit
7. Populate RecyclerView with an `Adapter` using `Glide.with(context).load(gifUrl).into(imageView)`

✅ Tip: Use `limit=25` and `api_key` in the query.

---

## 🔹 `CreateMemeFragment` – Upload Meme

### 🎯 Features:

* Pick meme from gallery or GIPHY
* Add caption overlay (via PhotoEditor or Canvas)
* Capture location
* Serialize to JSON and **POST to your API**

### 🧩 Implementation Steps:

1. Create layout: `fragment_create_meme.xml`

   * `ImageView`, `EditText`, `Button` for upload
2. Allow gallery selection using `Intent.ACTION_PICK`
3. Use `FusedLocationProviderClient` to get location
4. Overlay text on image:

   * Option 1: Use [`PhotoEditor`](https://github.com/burhanrashid52/PhotoEditor)
   * Option 2: Use `Canvas` on a custom `Bitmap`
5. Create a `MemePost` data class:

   ```kotlin
   data class MemePost(
       val userId: String,
       val imageUrl: String,
       val caption: String,
       val lat: Double,
       val lng: Double,
       val timestamp: String
   )
   ```
6. Send data via `POST /memes` using Retrofit

✅ Tip: Convert image to base64 if needed, or upload to Firebase Storage first and get the link.

---

## 🔹 `MapFragment` – View Memes on Map

### 🎯 Features:

* Uses **Google Maps SDK**
* Fetches memes from your API
* Places a **marker** for each geotagged meme

### 🧩 Implementation Steps:

1. Add Maps SDK + API Key to `AndroidManifest.xml`
2. Create layout: `fragment_map.xml` with `SupportMapFragment`
3. In `MapFragment.kt`:

   * Initialize the map in `onMapReady()`
   * Fetch memes from your API (GET `/memes`)
   * Loop through meme list:

     ```kotlin
     map.addMarker(MarkerOptions().position(LatLng(meme.lat, meme.lng)).title(meme.caption))
     ```
   * Center map on user’s current location using `FusedLocationProviderClient`

✅ Tip: Use a custom marker icon to display thumbnails.

---

## 🔹 `ProfileFragment` – User Memes + Sharing

### 🎯 Features:

* Lists memes posted by the current user
* Each item includes a **share button**

### 🧩 Implementation Steps:

1. Create layout: `fragment_profile.xml`

   * Use a `RecyclerView`
2. Create a `ProfileViewModel` to:

   * Call `GET /memes?userId=...`
3. Display memes in RecyclerView
4. For each item, add a “Share” button:

   * Use native `Intent.ACTION_SEND`:

     ```kotlin
     val shareIntent = Intent(Intent.ACTION_SEND)
     shareIntent.type = "text/plain"
     shareIntent.putExtra(Intent.EXTRA_TEXT, meme.caption + "\n" + meme.imageUrl)
     ```
5. You can optionally use Twitter SDK

✅ Tip: You can cache user ID using FirebaseAuth or SharedPreferences.

---

## 🧭 Suggested Folder Structure

```
MemeStreamApp/
├── ui/
│   ├── FeedFragment.kt
│   ├── CreateMemeFragment.kt
│   ├── MapFragment.kt
│   ├── ProfileFragment.kt
├── data/
│   ├── model/
│   │   └── Meme.kt, MemePost.kt
│   ├── network/
│   │   └── ApiService.kt
├── MainActivity.kt
├── navigation/
│   └── nav_graph.xml
```

---

## ✅ Summary

| Fragment             | Feature Summary                                                         |
| -------------------- | ----------------------------------------------------------------------- |
| `FeedFragment`       | Shows trending GIFs using GIPHY API, Moshi + Glide                      |
| `CreateMemeFragment` | Uploads meme, adds caption, geotags it, POSTs to your API               |
| `MapFragment`        | Loads memes from your API, shows them as markers on Google Map          |
| `ProfileFragment`    | Lists user's memes from API, includes share button (Intent/Twitter SDK) |

---
