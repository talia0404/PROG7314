# 🎉 MemeStream: Live Meme Feed (Setup Guide)
---

## 🌐 1. Use a RESTful API in your Android App  

https://github.com/talia0404/MemeStream 

1. **Pick & Inspect Your API**  
   - Review base URL, endpoints, HTTP methods, auth.  
   - hint: Get your URL that you're going to pull data from

## 🔑 1. Obtain & Include a Valid API Key

1. **Sign up** on the GIPHY Developers site (developer.giphy.com) and create an App to get your **API Key**.
2. **Verify** you’re inserting it correctly. If you’re using a URL‑query approach, your full request URL must look like:

   ```
   https://api.giphy.com/v1/gifs/trending?api_key=YOUR_REAL_KEY&limit=25
   ```
   
3. **Double‑check** there are no typos or extra characters in `YOUR_REAL_KEY`.

---

## ✅ Quick Checklist

* ✅ Did you **replace** `YOUR_REAL_KEY` with your actual GIPHY key?
* ✅ Did you **refresh** your emulator or device to clear any cached requests?
* ✅ Are you certain you’re hitting the **correct endpoint** (no extra slashes, correct domain)?

Once your key is valid, the API will return a 200 OK and you’ll get real meme instead of an empty arrau.

---
