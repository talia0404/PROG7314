# What is **Android Jetpack**? 🚀

A collection of official Android libraries, tools, and guidance from Google that help you build apps faster and with fewer bugs. They’re versioned independently of the OS, so you can ship features without waiting for Android releases.

Common Jetpack libraries you’ll use:

* **Lifecycle & ViewModel** – survive config changes and manage UI state.
* **Navigation** – type-safe navigation and back-stack handling.
* **Room** – local database on device.
* **DataStore** – key-value/proto storage (replacement for SharedPreferences).
* **WorkManager** – deferrable/background work.
* **Paging** – efficient infinite lists.
* **Hilt** – dependency injection.
* **CameraX**, **Compose**, **Glance** (widgets), testing libs, and more.

# What is **Jetpack Compose**? 🎨

Google’s modern **declarative** UI toolkit for native Android written in Kotlin.

* You describe UI with **@Composable** functions; the framework updates the screen when state changes.
* **Less XML/boilerplate**, powerful **Previews**, built-in **Material 3** theming, easy **animations** and **accessibility**.
* **Interoperates** with existing Views (you can mix Compose and XML).
* Scales from small components to entire apps.

Tiny example:

```kotlin
@Composable
fun Greeting(name: String) { Text("Hello, $name!") }
```

# What can you use them for? 🧩

* **End-to-end Android apps**: structure (MVVM with ViewModel), navigation, storage (Room/DataStore), background jobs (WorkManager), DI (Hilt).
* **Modern UIs with Compose**: forms, lists (LazyColumn), theming, animations, dialogs, snackbars, adaptive layouts for phones/tablets.
* **Performance & quality**: paging large feeds, CameraX for camera features, testing (JUnit/Espresso/Compose testing).

# When to choose what?

* **New app** → go **Compose-first**; it’s the current Android recommendation.
* **Existing XML app** → adopt **hybrid**: add Compose screens gradually while keeping legacy Views.
* Teaching/learning or prototyping → Compose speeds iteration and previewing.

https://developer.android.com/compose

https://developer.android.com/courses/jetpack-compose/course
