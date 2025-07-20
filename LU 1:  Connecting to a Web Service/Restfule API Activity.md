# Activity: **Random Joke Fetcher**

🎯 What you should do?
1. Make an HTTP GET request to a RESTful endpoint.
2. Parse the JSON response.
3. Update the UI with data fetched from the web.

1. **Project Setup**

   * Create a new Android project in Kotlin (minimum SDK 21).
   * In `activity_main.xml`, add:

     * A **Button** with text “Get Random Joke”
     * A **TextView** below it to show the joke

2. **Permissions**

   * In `AndroidManifest.xml`, add the Internet permission:

     ```xml
     <uses-permission android:name="android.permission.INTERNET"/>
     ```

3. **Networking Code**

   * In `MainActivity.kt`, inside the button’s click listener:

     1. Launch a background coroutine (or `AsyncTask`) to avoid blocking the UI thread.
     2. Build the URL:

        ```kotlin
        val url = URL("https://api.chucknorris.io/jokes/random")
        ```
     3. Open an `HttpURLConnection`, set method to `"GET"`, and timeouts (e.g. 10 000 ms).
     4. If `responseCode == 200`, read the `InputStream` into a string.
     5. Parse the JSON (e.g. `JSONObject(jsonString).getString("value")`).
     6. Post the joke text back to the main thread and set it on the TextView.

   * **Example snippet**:

     ```kotlin
     buttonFetch.setOnClickListener {
       CoroutineScope(Dispatchers.IO).launch {
         val connection = (URL("https://api.chucknorris.io/jokes/random")
           .openConnection() as HttpURLConnection).apply {
             requestMethod = "GET"
             connectTimeout = 10_000
             readTimeout    = 10_000
           }
         val joke = if (connection.responseCode == 200) {
           val text = connection.inputStream.bufferedReader().use { it.readText() }
           JSONObject(text).getString("value")
         } else {
           "Error: ${connection.responseCode}"
         }
         connection.disconnect()

         withContext(Dispatchers.Main) {
           textViewJoke.text = joke
         }
       }
     }
     ```
4. Links:

- Working with RESTful APIs in Android: Retrofit, Volley, OkHttp. Medium. 

URL:
https://medium.com/quick-code/working-with-restful-apis-in-android-retrofit-volley-okhttp-eb8d3ec71e06

- Android REST API Best Practices. Medium.

URL:
https://medium.com/@dugguRK/android-rest-api-best-practices-8385a61f39ea



