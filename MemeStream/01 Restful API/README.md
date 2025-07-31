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

> Replace `<username>` and `<password>` with your MongoDB Atlas credentials. You can get this connection string from [https://cloud.mongodb.com](https://cloud.mongodb.com)

---

### 🧠 5. **Define Meme model (`models/Meme.js`)**

```js
const mongoose = require('mongoose');

const MemeSchema = new mongoose.Schema({
  userId: { type: String, required: true },
  imageUrl: { type: String, required: true },
  caption: { type: String },
  lat: { type: Number },
  lng: { type: Number },
  timestamp: { type: Date, default: Date.now }
});

module.exports = mongoose.model('Meme', MemeSchema);
```

---

### 📡 6. **Create routes (`routes/memes.js`)**

```js
const express = require('express');
const router = express.Router();
const Meme = require('../models/Meme');

// GET all memes
router.get('/', async (req, res) => {
  try {
    const memes = req.query.userId
      ? await Meme.find({ userId: req.query.userId })
      : await Meme.find();
    res.json(memes);
  } catch (err) {
    res.status(500).json({ error: err.message });
  }
});

// POST new meme
router.post('/', async (req, res) => {
  try {
    const meme = new Meme(req.body);
    const saved = await meme.save();
    res.status(201).json(saved);
  } catch (err) {
    res.status(400).json({ error: err.message });
  }
});

module.exports = router;
```

---

### 🌐 7. **Create main server (`server.js`)**

```js
const express = require('express');
const mongoose = require('mongoose');
const cors = require('cors');
require('dotenv').config();

const app = express();
const PORT = process.env.PORT || 5000;

// Middleware
app.use(cors());
app.use(express.json());

// Routes
app.use('/memes', require('./routes/memes'));

// Connect to MongoDB
mongoose.connect(process.env.MONGO_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
}).then(() => {
  console.log('✅ Connected to MongoDB');
  app.listen(PORT, () => console.log(`🚀 Server running on http://localhost:${PORT}`));
}).catch(err => console.error('❌ MongoDB error:', err));
```

---

### 🧪 8. **Test your API with Postman**

Start your server:

```bash
node server.js
```

Then test:

* `GET http://localhost:5000/memes`
* `POST http://localhost:5000/memes` with JSON body:

```json
{
  "userId": "123abc",
  "imageUrl": "https://giphy.com/sample.gif",
  "caption": "Me right now",
  "lat": -29.85,
  "lng": 31.02
}
```

---

### ☁️ 9. **Host the API (free options)**

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


