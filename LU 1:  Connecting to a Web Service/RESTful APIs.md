🌐 **What is a RESTful API?**
  It’s an architectural style that uses standard HTTP methods (GET, POST, PUT, DELETE) to operate on “resources” identified by URLs. Responses are typically JSON (or XML) representations of those resources.

🔄 **Stateless & Uniform**
  Each request is independent (the server doesn’t keep session state), and all interactions follow the same pattern:

  1. Request → 2. Response
     You include everything you need (auth tokens, parameters) in each call.

🔑 **Key Uses**

  * **Decoupling** front‑end from back‑end—clients and servers can evolve separately
  * **Interoperability**—any platform that speaks HTTP/JSON can consume your API
  * **Scalability**—statelessness and caching let you add more servers easily
  * **Microservices & Integrations**—services talk to each other or to third‑party systems through simple HTTP calls

⚙️ **In Kotlin/Android**

  1. **Model your data** as `data class`es
  2. Pick a client:

     * **Retrofit** for declarative, type‑safe calls
     * **OkHttp** for lower‑level control
     * **Ktor** for multiplatform projects
  3. Make calls off the main thread (coroutines, callbacks)
  4. Handle status codes (2xx, 4xx, 5xx) and map JSON → objects

# **Connecting to a RESTful API**

A **RESTful API** is simply an HTTP service with a predictable URL structure and use of HTTP verbs (GET, POST, PUT, DELETE) to operate on “resources” .

### Example: AccuWeather five‑day forecast

1. **Build the base URL and query parameters**

   ```kotlin
   private const val BASE = 
     "https://dataservice.accuweather.com/forecasts/v1/daily/5day/305605"
   private const val API_KEY_PARAM = "apikey"
   private const val METRIC_PARAM  = "metric"

   fun buildWeatherUrl(): URL? {
     val uri = Uri.parse(BASE).buildUpon()
       .appendQueryParameter(API_KEY_PARAM, BuildConfig.ACCUWEATHER_API_KEY)
       .appendQueryParameter(METRIC_PARAM, "true")
       .build()
     return URL(uri.toString())
   }
   ```

   This uses Android’s `Uri` builder so you never have to worry about encoding “?” or “&” yourself ⁠.

2. **Fetch the data on a background thread**

   ```kotlin
   thread {
     val rawJson = try {
       buildWeatherUrl()?.readText()
     } catch (e: Exception) {
       null
     }
     runOnUiThread {
       // update your UI with rawJson
     }
   }
   ```

   Here, `URL.readText()` is a Kotlin extension that opens the connection, reads the stream, and closes it for you ⁠.

3. **Parse the JSON** (next steps)
   Once you have the JSON string, you can turn it into objects with `JSONObject`/`JSONArray` by hand, or use a library like Gson or Retrofit for automated mapping.

---

