# 🎉 MemeStream: Live Meme Feed (Setup Guide)
---

## 🌐 1. Use a RESTful API in an Android App  

1. **Pick & Inspect Your API**  
   - Review base URL, endpoints, HTTP methods, auth.  
   - hint: Get your URL that you're going to pull data from

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

