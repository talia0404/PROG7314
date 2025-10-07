# What “social media” integration means in Android 🍰

On Android you do two things:

* Share content through the system Share Sheet. This routes your image or video to any installed app like Instagram or TikTok. It uses an intent named `ACTION_SEND`. 
* Hand off files safely with a `FileProvider`. That creates a secure `content://` link so other apps can read your file without exposing your storage.

This combo already satisfies:

* LO5 connect to a social media service
* LO6 use a social media service
  because you integrate with the share system and actually post. If you want deeper, platform-specific features, you add each platform’s SDK later.

## 2) Resources  📚

* Android Share Sheet and `ACTION_SEND` quick guide. ([Android Developers][1])
* Secure file sharing setup with `FileProvider`, updated 10 Feb 2025. ([Android Developers][2])
* Media sharing patterns overview from Android team. ([Android Developers][3])
* Instagram “Sharing to Stories” and “Sharing to Feed” docs from Meta. ([developers.facebook.com][4])
* TikTok OpenSDK Share Kit quickstart and overview. ([developers.tiktok.com][5])

## 3) Do this first in Android Studio 🛠️

1. Add a share button in your layout, for example a Floating Action Button. When tapped, it will share an image or video.
2. Register a `FileProvider` in `AndroidManifest.xml` inside `<application>`:

```xml
<provider
    android:name="androidx.core.content.FileProvider"
    android:authorities="${applicationId}.provider"
    android:exported="false"
    android:grantUriPermissions="true">
    <meta-data
        android:name="android.support.FILE_PROVIDER_PATHS"
        android:resource="@xml/filepaths" />
</provider>
```

This is the official mechanism to pass a file to other apps. ([Android Developers][2])

3. Create `res/xml/filepaths.xml` so the provider knows which folders are shareable:

```xml
<?xml version="1.0" encoding="utf-8"?>
<paths>
    <cache-path name="cache" path="." />
    <files-path name="internal" path="." />
    <external-files-path name="external_files" path="." />
</paths>
```

These are common safe paths recommended for sharing. ([Android Developers][2])

4. In Kotlin, generate or pick your media file, get a `content://` URI from `FileProvider`, then fire the Share Sheet:

```kotlin
val file = /* your image or video file */
val uri = FileProvider.getUriForFile(this, "${packageName}.provider", file)
val intent = Intent(Intent.ACTION_SEND).apply {
    type = "image/*" // or "video/*"
    putExtra(Intent.EXTRA_STREAM, uri)
    addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)
}
startActivity(Intent.createChooser(intent, "Share"))
```

Android routes that to Instagram, TikTok, and others installed on the device. ([Android Developers][1])

## 4) Instagram path, two levels 🎯

### A) No SDK, fastest path via Share Sheet

Your `ACTION_SEND` flow above lets students post images to Instagram’s feed chooser. For a smoother Stories experience you can use Instagram’s Stories intent directly when Instagram is installed:

```kotlin
val insta = Intent("com.instagram.share.ADD_TO_STORY").apply {
    setDataAndType(uri, "image/*") // or "video/*"
    addFlags(Intent.FLAG_GRANT_READ_URI_PERMISSION)
    putExtra("source_application", packageName)
}
if (insta.resolveActivity(packageManager) != null) startActivity(insta)
```

This targets the documented “Sharing to Stories” contract. If not available, fall back to the generic Share Sheet. ([developers.facebook.com][4])

Meta’s docs also cover sharing to Feed if you prefer that route. 

Tips

* Always pass a `content://` URI from `FileProvider`, not a `file://` path. ([Android Developers][2])
* Videos should be MP4 with common codecs to maximize acceptance.

### B) With Instagram features later

If your students want stickers, background colors, or attributions, extend the Stories intent with extras as shown in Meta’s guide. Keep this as a stretch goal to avoid overwhelming first-timers. ([developers.facebook.com][4])

## 5) TikTok path, two levels 🎬

### A) No SDK, use Share Sheet

Many devices can hand videos to TikTok straight from the Share Sheet with the same `ACTION_SEND` flow. That is perfect for Theme 3 quick wins. ([Android Developers][1])

### B) With TikTok OpenSDK Share Kit

For a more controlled experience and better handoff, integrate Share Kit:

* Create a TikTok developer app, get your keys.
* Follow the Android Share Kit quickstart to add the SDK, request permissions, then call the share API with your video. ([developers.tiktok.com][5])

This gives nicer UX and future paths like login with TikTok if you want it in later themes.


---


[1]: https://developer.android.com/training/sharing/send?utm_source=chatgpt.com "Send simple data to other apps | App data and files"
[2]: https://developer.android.com/training/secure-file-sharing/setup-sharing?utm_source=chatgpt.com "Setting up file sharing | App data and files"
[3]: https://developer.android.com/social-and-messaging/guides/media-sharing?utm_source=chatgpt.com "About media sharing | Android social"
[4]: https://developers.facebook.com/docs/instagram-platform/sharing-to-stories/?utm_source=chatgpt.com "Sharing to Stories - Instagram Platform - Meta for Developers"
[5]: https://developers.tiktok.com/doc/share-kit-android-quickstart-v2?enter_method=left_navigation&utm_source=chatgpt.com "Share Kit for Android: Enabling TikTok Content Sharing"

