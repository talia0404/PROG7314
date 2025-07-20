An **HTTP connection** is the fundamental mechanism by which a client (your app) and a server exchange data over the web. At its core:

* **Protocol layer**: HTTP (Hypertext Transfer Protocol) sits at the application layer, riding over TCP/IP.
* **Request–response model**: The client opens a connection to the server’s URL, sends an HTTP request (method, headers, optional body), and then reads back the server’s HTTP response (status code, headers, body).
* **Statelessness**: Each request is independent; any context (authentication tokens, session IDs) must be re‑sent on every call.

---

## Uses of HTTP connections in Kotlin

Whether you’re writing a **JVM** application or an **Android** app, HTTP lets you:

1. **Consume RESTful APIs**

   * Fetch JSON or XML data from web services (e.g. weather, maps, social feeds)
   * Submit form data or JSON payloads via POST/PUT

2. **Upload and download files**

   * Download images, videos, documents at runtime
   * Upload user‑generated content (photos, logs) to a server

3. **Authenticate users**

   * Exchange credentials or tokens securely (OAuth, JWT)
   * Maintain session state via cookies or header tokens

4. **Real‑time or periodic data polling**

   * Poll a service for updates (e.g. chat messages, stock quotes)
   * Integrate webhooks or long‑polling mechanisms

5. **Service integration**

   * Call microservices in a backend architecture
   * Wire up to third‑party payment gateways, analytics, or notification services

---

## Common Kotlin approaches

* **Built‑in Java APIs**

  ```kotlin
  val url = URL("https://api.example.com/data")
  val conn = (url.openConnection() as HttpURLConnection).apply {
    requestMethod = "GET"
    connectTimeout = 10_000
    readTimeout    = 10_000
  }
  // handle conn.inputStream / conn.responseCode…
  conn.disconnect()
  ```

* **OkHttp** (Square’s HTTP client)

  ```kotlin
  val client = OkHttpClient()
  val request = Request.Builder().url("https://…").build()
  client.newCall(request).execute().use { response ->
    val body = response.body?.string()
    // …
  }
  ```

* **Retrofit** (Type‑safe REST client built on OkHttp)

  ```kotlin
  interface ApiService {
    @GET("users/{id}") suspend fun getUser(@Path("id") id: String): User
  }
  // Retrofit.Builder()… create(ApiService::class.java)
  ```

* **Ktor Client** (asynchronous, multiplatform)

  ```kotlin
  val client = HttpClient(CIO)
  val response: String = client.get("https://…")
  ```

---

