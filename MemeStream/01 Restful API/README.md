# 👨‍💻 STEP 1: Create Your Own RESTful API for MemeStream

Tech Stack: **Node.js + Express + MongoDB Atlas**

---
We're using VSCode

### 🗂️ 1. **Set up project folder**

In your project directory:

```bash
mkdir MemeStream
cd MemeStream
mkdir 01-RestfulAPI
cd 01-RestfulAPI
npm init -y
```

---

### 📦 2. **Install backend dependencies**

```bash
npm install express mongoose cors dotenv
```

> * `express`: Server framework
> * `mongoose`: MongoDB object modeling
> * `cors`: Cross-origin resource sharing
> * `dotenv`: To manage environment variables

---

### 📁 3. **Project structure**

Create the following files and folders:

```
01-RestfulAPI/
│
├── models/
│   └── Meme.js
├── routes/
│   └── memes.js
├── .env
├── server.js
├── package.json
```

---

### 🧾 4. **Create `.env` file**

```env
PORT=5000
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/memestream?retryWrites=true&w=majority
```

> Replace `<username>` and `<password>` with the **MongoDB database user** that you created **inside your cluster**, not your main Atlas login.

> 1. **Log in** to [https://cloud.mongodb.com](https://cloud.mongodb.com)
> 2. Go to your **Project** > **Clusters**
> 3. Click on your cluster → **Database Access** (left-hand menu)
> 4. Under **Database Users**, you'll see existing users or can **Create New User**

>   * **Username**: e.g., `memestream-user`
>   * **Password**: Set a secure password
>   * **Database Privileges**: Allow **Read and Write to any database**
> 5. Save the user

---

### 🧠 5. **Define Meme model (`models/Meme.js`)**

```js
// Import the mongoose library, which helps interact with MongoDB
const mongoose = require('mongoose');

// Define the structure (schema) for a Meme document in the MongoDB collection
const MemeSchema = new mongoose.Schema({
  // The unique ID of the user who created the meme
  userId: { type: String, required: true },

  // The URL of the meme image (from GIPHY or uploaded)
  imageUrl: { type: String, required: true },

  // Optional caption text added to the meme
  caption: { type: String },

  // Latitude where the meme was created (for geotagging)
  lat: { type: Number },

  // Longitude where the meme was created (for geotagging)
  lng: { type: Number },

  // Timestamp of when the meme was created; defaults to current time
  timestamp: { type: Date, default: Date.now }
});

// Export the Meme model so it can be used in other parts of the project
// This will create a "memes" collection in MongoDB
module.exports = mongoose.model('Meme', MemeSchema);
```

---

### 📡 6. **Create routes (`routes/memes.js`)**

```js
// Import the Express framework
const express = require('express');

// Create a new router instance
const router = express.Router();

// Import the Meme model we defined in Meme.js
const Meme = require('../models/Meme');


// GET /memes
// This endpoint fetches all memes from the database.
// If a `userId` is provided in the query string, it filters by that user.
router.get('/', async (req, res) => {
  try {
    const memes = req.query.userId
      ? await Meme.find({ userId: req.query.userId }) // Get memes by user
      : await Meme.find();                            // Get all memes

    // Return the memes as JSON
    res.json(memes);
  } catch (err) {
    // Return error response if something goes wrong
    res.status(500).json({ error: err.message });
  }
});


// POST /memes
// This endpoint allows a client (like your Android app) to upload a new meme.
// It expects a JSON body with userId, imageUrl, caption, lat, lng, timestamp.
router.post('/', async (req, res) => {
  try {
    // Create a new Meme document using the request body
    const meme = new Meme(req.body);

    // Save the meme to the database
    const saved = await meme.save();

    // Return the newly created meme with status 201 (Created)
    res.status(201).json(saved);
  } catch (err) {
    // Return validation or input errors
    res.status(400).json({ error: err.message });
  }
});


// Export this router so it can be used in server.js
module.exports = router;

```

---

### 🌐 7. **Create main server (`server.js`)**

```js
// Import required modules
const express = require('express');           // Web framework for building the API
const mongoose = require('mongoose');         // ODM library for MongoDB
const cors = require('cors');                 // Allows cross-origin requests (important for frontend-backend communication)
require('dotenv').config();                   // Loads environment variables from .env file

// Initialize the Express app
const app = express();

// Define the port from .env or default to 5000
const PORT = process.env.PORT || 5000;

// MIDDLEWARE SETUP

// Enable Cross-Origin Resource Sharing (e.g. allow Android app or browser to call the API)
app.use(cors());

// Enable parsing of JSON bodies in requests
app.use(express.json());

// ROUTE HANDLING

// All requests to /memes will be handled by the memes router
app.use('/memes', require('./routes/memes'));


// CONNECT TO MONGODB

// Connect to the MongoDB database using the connection string from .env
mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
})
.then(() => {
  // Log success message when connected
  console.log(' Connected to MongoDB');

  // Start the server only after a successful DB connection
  app.listen(PORT, () =>
    console.log(` Server running on http://localhost:${PORT}`)
  );
})
.catch(err => {
  // Log an error message if DB connection fails
  console.error(' MongoDB error:', err);
});

```

---

### 🧪 8. **Test your API with Postman**

#### 📦 Prerequisites

* Your Node.js server is running (i.e., `node server.js`)
* MongoDB Atlas is connected and working (check your `.env`)
* You’ve set up the `GET` and `POST` routes for `/memes`
* [Postman](https://www.postman.com/downloads/) is installed

---

#### 🔗 Request:

```
GET http://localhost:5000/memes
```

### 🧾 Instructions:

1. Open Postman.
2. Select `GET` from the dropdown.
3. Paste the URL: `http://localhost:5000/memes`
4. Click **Send**.

### ✅ You Should See:

```json
[
  {
    "_id": "64ff3b1aeff...",
    "userId": "abc123",
    "imageUrl": "https://...",
    "caption": "funny meme",
    "lat": -29.85,
    "lng": 31.02,
    "timestamp": "2025-07-31T..."
  },
  ...
]
```

---

## 🧪 2. Test `GET /memes?userId=abc123` – Filter by User

### 🔗 Request:

```
GET http://localhost:5000/memes?userId=abc123
```

1. Same as above, but add `?userId=abc123` in the URL
2. Click **Send**

✅ Response will be filtered by userId

---

### 🧪 3. Test `POST /memes` – Add a New Meme

#### 🔗 Request:

```
POST http://localhost:5000/memes
```

#### 🔧 Setup:

1. In Postman, select `POST`
2. URL: `http://localhost:5000/memes`
3. Go to the **Body** tab
4. Select **raw** and choose `JSON` (from dropdown)
5. Paste a test JSON object:

```json
{
  "userId": "abc123",
  "imageUrl": "https://media.giphy.com/media/xyz.gif",
  "caption": "Me after 2 hours of debugging",
  "lat": -29.85,
  "lng": 31.02
}
```

6. Click **Send**

#### ✅ You Should See:

```json
{
  "_id": "64ff3b1aeff...",
  "userId": "abc123",
  "imageUrl": "https://...",
  "caption": "Me after 2 hours of debugging",
  "lat": -29.85,
  "lng": 31.02,
  "timestamp": "2025-07-31T..."
}
```

---

#### ❗ Common Errors and Fixes

| Error Message               | Cause                             | Fix                                       |
| --------------------------- | --------------------------------- | ----------------------------------------- |
| `ECONNREFUSED`              | Server not running                | Run `node server.js`                      |
| `Cannot POST /memes`        | Route not connected               | Check `app.use('/memes', ...)`            |
| `400 Bad Request`           | Missing or invalid fields in JSON | Ensure all `required` fields are included |
| `500 Internal Server Error` | DB connection or logic error      | Check terminal for details                |


---

## ☁️ 9. **Host the API (free options)**

#### 🌍 Option 1: **Render**

1. Go to [https://render.com](https://render.com)
2. Connect your GitHub repo
3. Create new web service
4. Choose `01-RestfulAPI` folder
5. Set environment variables for `PORT` and `MONGO_URI`

#### 🌍 Option 2: **Railway**

* Go to [https://railway.app](https://railway.app)
* New Project → Deploy from GitHub or CLI

---

### ✅ You’re Done!

Your Android app can now use:

* `GET https://your-api/render.app/memes`
* `POST https://your-api/render.app/memes`

---


