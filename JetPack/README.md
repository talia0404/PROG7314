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

---

## 29 August 2025 (Group 2)/ 01 September 2025(Group 1) - JetPack Tutorial

**1. Do the compose essentials tutorial:**

https://developer.android.com/courses/jetpack-compose/course

### Step 2 - “Thinking in Compose” 🧠

* **Mindset shift (imperative → declarative):** you don’t “build and mutate views”; you **describe** what the UI should look like for the current state, and Compose re-draws it when state changes (recomposition). 
* **Composable functions as UI description:** small, side-effect-free functions that take data and **emit UI** by calling other composables; prefer immutability and predictable outputs.
* **Unidirectional data flow:** events bubble up (e.g., onClick), state updates happen in a state holder (often a ViewModel), and new state flows back down to the UI.
* **State hoisting:** keep the single source of truth above the composable that renders it; pass state + callbacks down, not mutable state around.
* **Why this matters:** simpler reasoning about UI, fewer bugs from stale/mutated view state, and easier testing.

### Step 3 - “Composable functions” 🧩

* **Building blocks of Compose:** a composable is a Kotlin function annotated to participate in composition; you compose UIs by **combining small reusable composables**.
* **Parameters & reusability:** pass in data and callbacks; avoid hidden globals; keep functions focused and stateless where possible (separate stateful/stateless versions).
* **Composition & recomposition basics:** Compose tracks what state was read; when that state changes, only the affected parts are recomposed — enabling efficient updates.
* **Modifiers & structure:** use modifiers to decorate/lay out elements and to keep UI concerns (padding, click, semantics) declarative and chainable.
* **Tooling highlights:** previews and other Compose tools accelerate iteration while you keep composables small and testable.

---

### XML/View World vs Jetpack Compose — Key Differences ⚖️

* **Mental Model**

  * **XML/View:** Imperative updates (call setters, manage visibility).
  * **Compose:** Declarative — describe UI for current **state**; framework updates UI.

* **UI Definition**

  * **XML/View:** Layouts in XML files + Java/Kotlin to mutate them.
  * **Compose:** UI in Kotlin functions (`@Composable`); no XML layouts for screens.

* **State & Data Flow**

  * **XML/View:** State often scattered (views, adapters, fragments).
  * **Compose:** Single source of truth (e.g., ViewModel); **unidirectional data flow** (events up, state down).

* **Updates & Performance**

  * **XML/View:** Manual invalidation/adapter notifications; risk of drift.
  * **Compose:** **Recomposition** only where state is read; minimal, targeted updates.

* **Lists**

  * **XML/View:** RecyclerView + Adapter + DiffUtil/notify calls.
  * **Compose:** `LazyColumn`/`LazyRow` with stable keys; no adapter boilerplate.

* **Tooling & Iteration**

  * **XML/View:** Layout Editor + preview (limited parity with runtime).
  * **Compose:** **Live Previews**, interactive previews, faster tweak-test loops.

* **Theming & Styling**

  * **XML/View:** Styles/themes via XML; mix of XML + code.
  * **Compose:** **Material 3** theming in Kotlin (color/typography/shape) applied consistently.

* **Interoperability**

  * **XML/View:** Native; Compose requires `ComposeView`.
  * **Compose:** Can host classic Views via interop or be hosted inside Views — gradual migration is supported.

* **Navigation**

  * **XML/View:** Fragments + NavController/graph XML.
  * **Compose:** **Navigation-Compose** with type-safe routes in Kotlin.

* **Testing**

  * **XML/View:** Espresso + View matchers.
  * **Compose:** Compose Testing APIs with semantics-driven selectors.

* **Boilerplate**

  * **XML/View:** More ceremony (findViewById/ViewBinding, adapters, XML).
  * **Compose:** Less boilerplate; more readable UI logic in one place.


**2. Stop after step 4: Writing your first compose app.**


