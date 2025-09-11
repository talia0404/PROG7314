# 🧭 What you’re building

A single-screen app called **QuickTasks** that:

* Shows a **Top App Bar** titled “QuickTasks” 🧭
* Lets you **type a task** and **add** it to a list ✍️➕
* Lets you **mark tasks done** ☑️
* Shows a **counter** “Completed: X / Y” 🔢
* Has a **FAB** that clears completed tasks and shows a **Snackbar** 🧹💬

---

## 0) Project prep  🛠️

1. Create a new Android project using **Empty Activity (Jetpack Compose)**.
2. Make sure your Gradle setup includes **Compose** and **Material 3** (BOM + material3). If unsure, skim the “Get started with Compose” page and the Material 3 overview to confirm artefact names and versions.
3. Run the template app once to confirm your emulator/device is good.

---

## 1) Replace the screen content (MainActivity) 📄

1. Open your **`MainActivity.kt`**.
2. Replace its content with the **starter** you were given (the one in your message).

   * It defines:

     * A `Task` data holder
     * A root `QuickTasksApp()` composable
     * A `TaskItem(...)` row
     * A preview function
3. Clean/rebuild the project to let Android Studio **auto-import** what’s missing. If you see unresolved imports for Material 3, verify you’re using the **Material 3** artefacts (not Material 2). The Material 3 release page and component docs show the correct package names. 

**Why this matters:** You’re switching from the default template to your own **Compose tree**. Compose doesn’t inflate XML—your UI is built by calling composable functions.

---

## 2) Understand the scaffolded layout 🧱

Open `QuickTasksApp()` and identify its parts:

* **Scaffold** provides page structure (top bar, FAB, snackbar host, and content slot). Read its overview to learn which “slots” it gives you and how **content padding** is passed down. 
* **Top App Bar** displays the screen title. Review the app bar docs for structure and properties (title, actions, navigationIcon, colours, scrollBehavior). 
* **FAB** will clear completed tasks.
* **SnackbarHost** shows transient messages after the clear action. Learn how `SnackbarHostState` and `showSnackbar(...)` work together. 

✅ **Checkpoint:** You can point at each slot (top bar, content, FAB, snackbar host) and explain what goes where.

---

## 3) Wire up **state** for input & list 🔄

In `QuickTasksApp()`, you’ll see two pieces of state:

* `input` → the text the user typed
* `tasks` → the list of Task items

Read **State in Compose** to understand:

* Why UI **recomposes** when state changes
* Why `remember { ... }` stores state across recompositions (but not rotations)
* How `rememberSaveable` persists across configuration changes (you’ll switch to this later) 

✅ **Checkpoint:** Type, add, and toggle tasks; watch the UI update automatically. Be able to explain “recomposition”: *when a state read by a composable changes, Compose re-invokes that composable to update the UI*. 

---

## 4) Build the **input row** and **counter** ✍️➕🔢

* The input row uses a **text field** and an **Add** button from **Material 3**. Skim the Material 3 component catalogue for names and key parameters (labels, enabled state, shape, etc.). 
* The counter text (“Completed: X / Y”) depends on `tasks`. When you add/toggle tasks, it updates automatically thanks to state-driven UI. Review the State guide for that mental model. 

✅ **Checkpoint:** After adding a few tasks and toggling one as done, the counter should reflect it accurately.

---

## 5) Display tasks with **LazyColumn** 📜

* Use **LazyColumn** for efficient, scrollable lists. Understand why Lazy layouts only compose what’s visible and why **stable keys** help prevent item state mismatch and improve performance. 
* Each row uses a lightweight **Card** with a **Checkbox** + **Text**. See Material 3 component docs to confirm guidance on density, spacing, and semantics.

✅ **Checkpoint:** The list scrolls smoothly; toggling a checkbox updates only that row and the counter. You can explain why a **Column** isn’t ideal for long lists vs **LazyColumn**.

---

## 6) Clear completed with **FAB + Snackbar** 🧹💬

* The FAB triggers a **filter** that removes completed tasks, then shows a **Snackbar** summary (“Cleared N task(s)”).
* Learn the correct pattern:

  * A **`SnackbarHostState`** owned near the Scaffold
  * A **composition-aware coroutine scope** (see **`rememberCoroutineScope`**)
  * Calling **`showSnackbar(...)`** to display the message
    Walk through the official Snackbar docs and the side-effects page for when to use `rememberCoroutineScope` vs `LaunchedEffect`. 

✅ **Checkpoint:** When there are completed tasks, tapping the FAB removes them and shows a snackbar. If nothing is completed, show a different message (your copy choice).

---

## 7) Make state survive **rotation** with `rememberSaveable` 🔄📱

* Right now, `remember` will **not** persist across configuration changes (rotation, locale).
* Switch to **`rememberSaveable`** for `tasks` and `input`. Start with the **Save UI state** guide for strategies. If you store **custom types**, read the section on **Savers** (how to flatten and restore) and decide how you’d serialize your `Task` to be saveable. 

✅ **Checkpoint:** Add some tasks, rotate the device/emulator; the list and input still show exactly as before. Be ready to articulate the difference between `remember` and `rememberSaveable`. 

---

## 8) Preview your UI fast 🖼️⚡

* Add **Previews** to iterate without installing to a device every time. The Preview docs explain how to annotate composables, set device sizes, and render dark mode. 
* Explore **Tooling for Compose** for extra productivity (Animation Preview, interactive preview, etc.).

✅ **Checkpoint:** You can render at least one Preview of the main screen (and ideally a second with a different UI state).

---

## 9) Accessibility & polish ♿️🎨

* Ensure interactive controls have meaningful **content descriptions** (or are decorative). Material 3 docs explain recommended semantics and default sizes/spacing. 
* Move visible strings into **resources** for future localization.
* Verify **touch targets** and spacing feel comfortable.

---

# 🧪 Quick self-test (students)

1. In your own words: *What triggers a recomposition in Compose?*
2. When would you pick `remember` vs `rememberSaveable`? Give one concrete example for each. 
3. Why is `LazyColumn` preferred over `Column` for long lists? What are **stable keys** for? 
4. Why does showing a Snackbar require a coroutine? When should you use `rememberCoroutineScope` vs `LaunchedEffect`? 
5. Which Scaffold slot is responsible for Snackbars? How is padding passed to your content?

---

# 📚 Exact places to find the code (official, up-to-date)

* **State & recomposition**: *State and Jetpack Compose* (incl. `remember`, state hoisting). 

"State and Jetpack Compose" - Android Developers: https://developer.android.com/develop/ui/compose/state

* **Saving state**: *Save UI state in Compose* (`rememberSaveable`, Savers). 

"Save UI state in Compose" - Android Developers: https://developer.android.com/develop/ui/compose/state-saving  

* **Lists**: *Lists and grids* (`LazyColumn`, keys, item APIs). 

"Lists and grids | Jetpack Compose" - https://developer.android.com/develop/ui/compose/lists

* **Material 3 components & Scaffold**: Component catalog & release notes (TopAppBar, FAB, TextField, Card). 

 "Compose Material 3 | Jetpack": https://developer.android.com/jetpack/androidx/releases/compose-material3 

* **Snackbar**: Component guide (host, host state, `showSnackbar(...)`). 

 "Snackbar | Jetpack Compose": https://developer.android.com/develop/ui/compose/components/snackbar

* **Side-effects**: *Side-effects in Compose* (`rememberCoroutineScope`, `LaunchedEffect`).

 "Side-effects in Compose": https://developer.android.com/develop/ui/compose/side-effects 

* **Previews**: *Composable previews* guide; *Tools for Compose* hub. 

"Preview your UI with composable previews": https://developer.android.com/develop/ui/compose/tooling/previews 

* **Compose basics & getting started**: Central Compose docs landing page.

Android Developers - "Get started with Jetpack Compose", https://developer.android.com/develop/ui/compose/state

* **App bars guidance** (structure, behaviours, patterns): App bar component page (Compose) and Material 3 guidelines.

 "App bars | Jetpack Compose": https://developer.android.com/develop/ui/compose/components/app-bars
 "Top app bar – Material Design 3": https://m3.material.io/components/app-bars/guidelines  

 repo link:  https://github.com/talia0404/02-QuickTasks.git
