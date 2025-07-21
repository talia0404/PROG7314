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

## Resaurant analogy:

Think of a RESTful API like dining at a restaurant 🍽️:

---

### 1. The Restaurant (Server) 🏨

* **Role:** Prepares and serves food, manages the kitchen.
* **In REST:** The server stores your data and runs the business logic.

### 2. The Menu (Resource Catalog) 📖

* **Role:** Lists all dishes you can order.
* **In REST:** The set of URIs (e.g. `/users`, `/orders`, `/products`) that identify each resource.

### 3. The Waiter (Endpoint) 🧑‍🍳➡️👩‍💼

* **Role:** You tell the waiter your order; they relay it to the kitchen and bring back your food.
* **In REST:** The client sends an HTTP request to an endpoint; the server processes it and returns data.

### 4. Placing Your Order (HTTP Methods) 🍔➡️

| Restaurant Action | HTTP Method   | What It Means                                      |
| ----------------- | ------------- | -------------------------------------------------- |
| Ask to see a dish | **GET**       | “Bring me that item.”                              |
| Order a new dish  | **POST**      | “I’d like to add this to my table.”                |
| Change your order | **PUT/PATCH** | “Swap my side salad for fries” (replace vs tweak). |
| Send a dish back  | **DELETE**    | “Please remove it from my bill.”                   |

> **Idempotent**: Repeating the same request (e.g. cancelling the same dish) has no extra effect after the first time.

### 5. Stateless Service 🤝

* **In the Restaurant:** Every time you call the waiter, you remind them of your table number and order—no “memory” between calls.
* **In REST:** Each HTTP request must include all needed info (credentials, parameters); the server doesn’t store session state.

### 6. Cacheable Responses ⚡

* **In the Restaurant:** If the soup of the day hasn’t changed, the waiter can confirm quickly instead of checking the kitchen every time.
* **In REST:** Responses include headers (`Cache-Control`, `ETag`) so clients or proxies can reuse them and speed things up.

### 7. Layered System 🏗️

* **In the Restaurant:** You talk to the waiter → supervisor → kitchen. You never deal directly with the cook.
* **In REST:** Clients talk to API gateways or load balancers, which route to application servers or caches behind the scenes.

### 8. Hypermedia Links (HATEOAS) 🔗

* **In the Menu:** Next to each dish, QR codes suggest side dishes or pairings.
* **In REST:** Responses embed links to related resources (`"orders": "/users/123/orders"`) so clients discover next steps dynamically.

---


