# 🎉 MemeStream: Live Meme Feed (Setup Guide)
---

## 🌐 1. Use a RESTful API in an Android App  

https://github.com/talia0404/MemeStream 

1. **Pick & Inspect Your API**  
   - Review base URL, endpoints, HTTP methods, auth.  
   - hint: Get your URL that you're going to pull data from

## 🔑 1. Obtain & Include a Valid API Key

1. **Sign up** on the GIPHY Developers site (developer.giphy.com) and create an App to get your **API Key**.
2. **Verify** you’re inserting it correctly. If you’re using a URL‑query approach, your full request URL must look like:

   ```
   https://api.giphy.com/v1/gifs/trending?api_key=YOUR_REAL_KEY&limit=25
   ```
   
3. **Double‑check** there are no typos or extra characters in `YOUR_REAL_KEY`.

---

## ✅ Quick Checklist

* ✅ Did you **replace** `YOUR_REAL_KEY` with your actual GIPHY key?
* ✅ Did you **refresh** your emulator or device to clear any cached requests?
* ✅ Are you certain you’re hitting the **correct endpoint** (no extra slashes, correct domain)?

Once your key is valid, the API will return a 200 OK and you’ll get real meme instead of an empty arrau.

---

2. **Configure Networking**  
   - Add Retrofit (or OkHttp) to Gradle.  
   - ⚠️ **Tip:** Centralise your base URL in one constant.
     
     ```kotlin
     companion object {
       const val BASE_URL = "url"
     }
     ```
     
3. **Async Calls**  
   - Always run on a background thread (coroutines/Dispatchers.IO).

---

## 🗃️ 2. Use JSON Objects to Read Data  

1. **Review JSON Structure**  
   - Hit the endpoint in Postman/browser and copy its sample JSON.

2. **Define Your Models**  
   - Create Kotlin `data class`es matching the JSON keys.  
   - **Example** for nested objects:

      ```kotlin
     @JsonClass(generateAdapter = true)
     data class Gif(
       val id: String,
       val title: String,
       val images: ImageVariants
     )
     ```

4. **Parse with Moshi/Gson**  
   - Moshi adapter converts JSON → your classes.

---

## 🔄 3. Use JSON Objects to Write Data Back  

1. **Design Your Request Schema**  
   - Sketch the JSON you need to send (fields + types).

2. **Create Request Models**  
   - Define another `data class` for the payload.  
   - **Example** of serialisation:
   - 
     ```kotlin
     val json = moshi.adapter(Meme::class.java).toJson(myMemeObject)
     ```

3. **POST Your JSON**  
   - Attach the JSON string to your HTTP POST; set header `Content-Type: application/json`.

---

## 🤝 4. Use a Library to Work with JSON (Moshi/Gson)  

1. **Add Dependency**
   
   ```kotlin
   implementation ("com.squareup.moshi:moshi-kotlin:1.14.0")
   kapt ("com.squareup.moshi:moshi-kotlin-codegen:1.14.0")

---

2. **Configure Adapter**

   * Instantiate a single `Moshi` or `Gson` object in a shared module.

3. **Annotate Fields**

   * If JSON names differ, use annotations:

     ```kotlin
     @Json(name="user_name") val userName: String
     ```

---

## 🧩 5. Apply Fragments to Structure Your UI

1. **Identify Screens**

   * e.g. **Feed**, **Create**, **Map**, **Profile**

2. **Create Fragment + Layout**

   * Each screen gets a `Fragment` subclass + `fragment_*.xml` layout.

3. **Host in Activity**

   * One `MainActivity` with a container (`FrameLayout` or `NavHostFragment`).

4. **Switch Fragments**

   * **Minimal snippet** for manual transaction:

     ```kotlin
     supportFragmentManager.beginTransaction()
       .replace(R.id.container, DetailFragment().apply {
         arguments = bundleOf("memeId" to id)
       })
       .commit()
     ```

5. **Pass Data Between Fragments**

   * Use `Bundle` arguments or a shared `ViewModel`.

---

### ✅ What should be accomplished:

* 🌐 **API Setup**: Base URL constant, Retrofit/OkHttp added
* 🗃️ **JSON Read**: Data classes matching JSON, Moshi/Gson adapter
* 🔄 **JSON Write**: Request models, serialization snippet
* 🤝 **JSON Library**: Dependency + annotations configured
* 🧩 **Fragments**: Fragments created, hosted, and navigable

