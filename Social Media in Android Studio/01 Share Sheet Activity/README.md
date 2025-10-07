#  😎📲 Connect to social media

A tiny app that shares an image or video from the app into another app using Android’s Share Sheet. You will tap a Share button, choose Instagram or TikTok, and post. 

---

# 1) Project setup in Android Studio 🧱

---

# 2) Gradle configuration ⚙️

Open the following files and confirm or set these values. Do not paste code, just check and edit as needed.

## a) `settings.gradle.kts`

* Ensure your project name is set.
* Re-sync after changes.

## b) `build.gradle.kts` (Project)

* Make sure Google’s Maven and Maven Central repositories are listed.

## c) `app/build.gradle.kts`

* `compileSdk` and `targetSdk` should be recent. Use the latest installed in your SDK Manager.
* `minSdk` at least 24.
* Enable View Binding if you are using views.
* Dependencies to confirm:

  * AndroidX core
  * AppCompat
  * Material Components
* Sync Gradle when done.

---

# 3) Manifest setup for safe file sharing 🛡️

You will share a file with other apps. Android requires a `FileProvider` for safe access.

1. Open `AndroidManifest.xml`.
2. Inside the `<application>` element, declare a `provider` that uses `androidx.core.content.FileProvider`.
3. Set the `authorities` to `${applicationId}.provider`.
4. Link a meta-data resource named `@xml/filepaths`.
5. Save the file.

Why this matters: other apps can read your shared file via a secure `content://` URI without exposing your internal storage.

---

# 4) Create the FileProvider paths 📁

1. Create a new directory `res/xml` if it does not exist.
2. Add a resource file named `filepaths.xml`.
3. Add entries for:

   * `cache-path` for temporary images or videos generated at runtime
   * `files-path` if you plan to save into internal files
   * `external-files-path` if you save media into the app’s external files directory

Advice: For a simple demo, use `cache-path`. It needs no storage permission and is perfect for one-time shares.

---

# 5) Layout for the demo UI 🎛️

1. Open `res/layout/activity_main.xml`.
2. Add:

   * A title TextView that says something like “Share to Socials”.
   * A description TextView that explains the flow in one line.
   * A Button or FloatingActionButton labeled “Share”.
3. Position with ConstraintLayout so it looks neat.
4. Save.

Add a preview image in the layout to hint what will be shared.

---

# 6) Strings and icons 🏷️

1. In `res/values/strings.xml`, add strings for:

   * App name
   * Share button text
   * Chooser title, for example “Share to…”
2. In `res/drawable`, add a generic share icon if you want a FAB. Android Studio has built-in vector assets.

---

# 7) The share flow you will implement 🧩

Write the code, but here is the exact flow they must follow when they press Share:

1. Prepare content to share.

   * Option A image: generate or load a bitmap and save it into the app `cache` directory.
   * Option B video: copy a small MP4 from `raw` resources into `cache` so it is a real file on disk.
2. Ask `FileProvider` for a `content://` URI using the same authority string as in the manifest.
3. Create an `ACTION_SEND` intent.

   * Set the MIME type to `image/*` for images or `video/*` for videos.
   * Put the `content://` URI into the extras.
   * Grant temporary read permission on the intent.
4. Start a chooser so the user picks Instagram or TikTok.

   * If a platform is missing from the list, it is not installed or the MIME type does not match what the app accepts.

That is all the logic needed to connect and use a social media app from your app.

---

# 8) Direct Instagram Stories route 🎯

You can add a second button labelled “Share to Instagram Stories” that attempts a direct handoff:

1. Create an intent with the documented Instagram Stories action.
2. Set the data and MIME type to match your image or video.
3. Grant read permission on the URI.
4. Before launching, check that an app can handle this action.
   If the device cannot resolve it, fall back to the generic Share Sheet.

This shows platform-specific routes while still keeping the main lab simple.

---

