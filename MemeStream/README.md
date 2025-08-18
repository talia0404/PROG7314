# 🎉 **MemeStream: Live Meme Feed**

## 🌟 What is MemeStream?  
MemeStream is a fun, social Android app where users can:
- **Browse** trending GIF memes from GIPHY  
- **Caption** or upload their own memes  
- **Geotag** each creation with their current location  
- **View** all memes on an interactive map  
- **Share** favorite memes to Twitter, Instagram, etc.  

All of this is done in a modular app using modern Android best practices!

---

## 🎯 Why We’re Building This  
By creating MemeStream, you will learn to:
1. **Connect** to web services via RESTful APIs 🌐  
2. **Parse** and **produce** JSON payloads 🗃️  
3. **Organize** your UI with Fragments 🧩  
4. **Leverage** external libraries (Glide, Moshi) 🤝  
5. **Obtain** and **display** geolocation data 📍  
6. **Integrate** social‑sharing SDKs (Twitter Kit, Maps SDK) 📲  

This hands‑on project ties together all the module’s Learning Outcomes in one cohesive, real‑world app!

---

## 📚 Learning Outcomes Covered  
1. **Use a RESTful API** in an Android app  
2. **Use JSON objects to read data** from a service  
3. **Use JSON objects to write data** back to a service  
4. **Use a library to work with JSON data** (Moshi/Gson)  
5. **Apply Fragments** to structure your UI  
6. **Use an external library** to solve a programming problem (Glide for GIFs)  
7. **Connect to a geolocation service** (FusedLocationProviderClient)  
8. **Display information from a geolocation service** on a map (Google Maps SDK)  
9. **Connect to a social media service** (Twitter Kit or Facebook Share)  
10. **Use a social media service** API/SDK to post content  
11. **Survey available SDKs** relevant to the app  
12. **Integrate an appropriate SDK** (e.g. Twitter Kit, Google Maps)  

---

## 🛠️ Implementation Steps

### 1. 🚀 Project Setup  
- **New Android Project** (Kotlin, min SDK 21)  
- **Permissions** 

---

### 2. 🧩 Design Your Fragments

* **FeedFragment**

  * Shows trending memes in a `RecyclerView`
  * Uses **Retrofit + Moshi** to GET GIPHY JSON
  * Loads GIFs via **Glide**
* **CreateMemeFragment**

  * Pick/upload or select a GIF
  * Add text overlay (e.g. PhotoEditor library)
  * Fetch current `lat/lng` via **FusedLocationProviderClient**
  * Serialize `{ userId, imageUrl, caption, lat, lng, timestamp }` with Moshi
  * POST to Firestore REST or your backend
* **MapFragment**

  * Embed **Google Maps SDK**
  * GET user‑created memes, place a Marker for each geotag
* **ProfileFragment**

  * List user’s own memes (Firestore GET)
  * Each item has a **Share** button

---

### 3. 🌐 RESTful API Integration

* **Trending Feed**:

* **User Memes**:

  * **GET** `/memes` → list user memes
  * **POST** `/memes` → save new meme JSON payload

---

### 4. 🗃️ JSON Read & Write with Moshi

* **Data classes** mirror API schemas:

* **Serialize** user meme:

---

### 5. 📍 Geolocation & Maps

* **FusedLocationProviderClient** to get last known location
* **GoogleMap.addMarker()** for each meme’s coordinates
* Center the map on the user’s current position

---

### 6. 📲 Social Sharing

* **Twitter Kit**: configure in `Application` class
* In **ProfileFragment**, on “Share” tap

---

