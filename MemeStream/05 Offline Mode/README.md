# 🔹 Step 5: Enable Offline Mode with RoomDB

1. **Add RoomDB Setup** 🏠

   * Define a local database that can store memes (id, caption, image URL/path, location, timestamp, userId).
   * This mirrors the structure of your API, so syncing will be easier later.

2. **Use DAO for CRUD Operations** ✍️

   * Create data access methods (insert, delete, update, query) for memes.
   * These will let your app save memes offline when the API can’t be reached.

3. **Repository Layer** 📦

   * Have a repository that decides:

     * If online → use Retrofit (API).
     * If offline → use RoomDB.
   * This ensures a seamless experience for the user.

4. **Sync Strategy** 🔄

   * When the device goes back online:

     * Compare local unsynced memes with the server.
     * Push new memes to the API.
     * Fetch the latest memes and update RoomDB.

5. **Background Worker (Optional but Recommended)** ⏰

   * Use WorkManager to automatically retry sync when the device is online again.
   * This way, the user doesn’t have to manually refresh.

6. **User Feedback** 🖼️

   * Show cached memes immediately when offline (RecyclerView backed by RoomDB).
   * Indicate sync status (e.g., “pending upload” tag on unsynced memes).

---

### ✅ What You’ll Achieve

* Your app will no longer “break” when there’s no internet.
* Users can **create and view memes offline**.
* Once online, all memes are synced automatically.

---
