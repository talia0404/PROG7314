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
  * **Compose:** **Material 3** theming in Kotlin (colour/typography/shape) applied consistently.

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

### Step 3: ✨📱 Jetpack Compose Basics – Tutorial Summary

---

📝 1. **Before You Begin**

* Jetpack Compose = modern, declarative UI toolkit using Kotlin and composable functions (`@Composable`) to build UI.
* Tutorial uses **Material 3** → students should stick to Material 3 for modern projects.

🚀  Notes 

✅ Use **Material 3** (`androidx.compose.material3.*`).

✅ Prefer `animateContentSize()` for expanding cards.

✅ Keep dependencies updated with the latest Compose BOM.

✅ Test in both **light & dark modes**.

✅ Use **string resources** instead of hardcoded text for accessibility.

---

🆕 2. **Start a New Compose Project**

* In Android Studio → choose **Empty Activity**, set `minSdk ≥ 21`.
* Project already includes Compose setup → open `MainActivity.kt`.

---

🎨 3. **Explore Composable Functions**

* Build UI with `@Composable` functions.
* Preview with `@Preview` annotation.

---

🎨🖌️ 4. **Tweak the UI**

* Use `Surface` for backgrounds + theming.
* Add spacing & styling with `Modifier` (e.g., `.padding()`).

---

🔁 5. **Reusable Composables**

* Create `MyApp` composable to reduce duplication and keep code clean.

---

📐 6. **Layouts: Column, Row, Box**

* Arrange elements vertically with `Column`, horizontally with `Row`, and overlay with `Box`.

---

## 🔘 7. **Add a Button**

* Add an `ElevatedButton`.
* Use `.weight(1f)` in a `Row` for spacing between items.

---

🔄 8. **State Management**

* Manage UI state with `remember { mutableStateOf(...) }`.
* Use `by` delegation for cleaner syntax (`var expanded by remember { ... }`).

---

🏗️ 9. **Hoist State**

* Move state up to a parent composable.
* Pass down callbacks like `onContinueClicked`.

---

📜 10. **Use LazyColumn for Performance**

* For long lists → use `LazyColumn { items(...) { ... } }`.
* Much more efficient than a normal `Column`.

---

💾 11. **Persisting State**

* Use `rememberSaveable` to keep state (like expanded/collapsed) after rotation.

---

🎬 12. **Add Animation**

* Animate padding or size changes with `animateDpAsState` or `animateContentSize()`.
* Add smooth effects with `spring()`.

---

🎨🌙 13. **Styling & Theming**

* Explore `Theme.kt`: support dark/light modes + dynamic colour.
* Apply typography styles (e.g. `headlineMedium`).
* Use `@Preview(..., uiMode = UI_MODE_NIGHT_YES)` to test dark mode.

---

🎉 14. **Finishing Touches**

* Replace text buttons with `IconButton + Icon`.
* Wrap UI in a `Card` for polished Material 3 look.
* Always include `contentDescription` for accessibility.


---

# 📊 Quick At-A-Glance Version for You

| Step | What to Do                                           | Pro Tip                             |
| ---- | ---------------------------------------------------- | ----------------------------------- |
| 1️⃣  | Set up Compose project with Material 3               | Use latest Android Studio           |
| 2️⃣  | Build UI with `@Composable`, preview with `@Preview` | Cleaner Kotlin with `by` delegation |
| 3️⃣  | Style with `Surface`, `Modifier`, and theming        | Keep UI reusable                    |
| 4️⃣  | Layout with `Column`, `Row`, `.weight()`             | Organise properly                   |
| 5️⃣  | Manage state with `rememberSaveable`                 | Hoist state + callbacks             |
| 6️⃣  | Use `LazyColumn` for lists                           | More efficient than `Column`        |
| 7️⃣  | Animate with `animateContentSize()`                  | Simpler & smoother                  |
| 8️⃣  | Polish with `Card`, icons, dark mode                 | Test accessibility too              |

---


