<p align="center">
  <img src="https://ik.imagekit.io/hassaan/Code_Snippets_By_HMK_CodeWeb_nz6EWS0Va" width="100%" height="400"  alt="Project Logo"/>
</p>

# Code Snippets

A free collection of useful **basic to advanced** code snippets for Programmers 🐱‍👤.

Copy → Paste → Use. .

---

# 📦 Table of Contents (30 Snippets)

1. [Smooth Scroll to Section](#1-smooth-scroll-to-section)
2. [Copy to Clipboard](#2-copy-to-clipboard)
3. [Detect + Toggle Dark/Light Mode](#3-detect--toggle-darklight-mode)
4. [Fetch POST Request](#4-fetch-post-request)
5. [Fetch GET With Error Handling](#5-fetch-get-with-error-handling)
6. [Axios POST With Headers](#6-axios-post-with-headers)
7. [Express Basic Server](#7-express-basic-server)
8. [Express Middleware: Auth Check](#8-express-auth-middleware)
9. [MongoDB Connection](#9-mongodb-connection)
10. [Create Mongoose Model](#10-create-mongoose-model)
11. [JWT Token Generate](#11-generate-jwt-token)
12. [JWT Middleware Verify](#12-verify-jwt-token)
13. [Password Hashing (bcrypt)](#13-password-hashing-bcrypt)
14. [File Upload With Multer](#14-file-upload-with-multer)
15. [Rate Limiting Middleware](#15-rate-limiting-middleware)
16. [CORS Setup](#16-cors-setup)
17. [React Fetch Hook](#17-react-fetch-hook)
18. [React Debounce Hook](#18-react-debounce-hook)
19. [React LocalStorage Hook](#19-react-localstorage-hook)
20. [React Protected Route](#20-react-protected-route)
21. [Scroll to Top on Route Change (React)](#21-scroll-to-top-react)
22. [Tailwind Modern Card UI](#22-tailwind-modern-card)
23. [Reels Feed UI React Tailwindcss](#23-reels-feed-ui-react-tailwindcss)
24. [CSS Glassmorphism UI](#24-css-glassmorphism)
25. [LocalStorage With Expiry](#25-localstorage-with-expiry)
26. [Generate Unique IDs](#26-generate-unique-ids)
27. [Validate Email](#27-validate-email)
28. [Download File from URL](#28-download-file-url)
29. [Throttle Function](#29-throttle-function)
30. [Debounce Function](#30-debounce-function)
31. [Custom Scroll bar Css](#31-custom-scroll-bar-css)
32. [Cloudinary ImageUploader SetUp](#32-cloudinary-imageuploader-setup)
33. [Request Logger](#33-request-logger)

---

# 1. Smooth Scroll to Section

```js
document.querySelectorAll("[data-scroll]").forEach((btn) => {
  btn.addEventListener("click", () => {
    document
      .querySelector(btn.dataset.scroll)
      .scrollIntoView({ behavior: "smooth" });
  });
});
```

---

# 2. Copy to Clipboard

```js
navigator.clipboard.writeText("Copied text!");
```

---

# 3. Detect + Toggle Dark/Light Mode

```js
const systemDark = window.matchMedia("(prefers-color-scheme: dark)").matches;

function applyTheme(t) {
  document.documentElement.dataset.theme = t;
  localStorage.setItem("theme", t);
}

applyTheme(localStorage.getItem("theme") || (systemDark ? "dark" : "light"));

function toggleTheme() {
  const current = document.documentElement.dataset.theme;
  applyTheme(current === "dark" ? "light" : "dark");
}
```

---

# 4. Fetch POST Request

```js
async function postData() {
  const res = await fetch("/api/user", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ name: "Hassan", age: 21 }),
  });

  const data = await res.json();
  console.log(data);
}
```

---

# 5. Fetch GET With Error Handling

```js
async function getData() {
  try {
    const res = await fetch("/api/products");
    if (!res.ok) throw new Error("Failed request");
    return await res.json();
  } catch (e) {
    console.error(e);
  }
}
```

---

# 6. Axios POST With Headers

```js
axios.post(
  "/api/login",
  {
    username: "admin",
    password: "1234",
  },
  {
    headers: { Authorization: "Bearer token" },
  }
);
```

---

# 7. Express Basic Server

```js
import express from "express";
const app = express();
const PORT = process.env.PORT || 3000;

app.get("/", (req, res) => res.send("API Running"));

app.listen(PORT, () => console.log(`Server Running on ${PORT}`));

```

---

# 8. Express Auth Middleware

```js
function auth(req, res, next) {
  if (!req.headers.token) return res.status(401).send("Unauthorized");
  next();
}
export default auth;
```

---

# 9. MongoDB Connection

```js
import mongoose from "mongoose";

const connectDB = async () =>{
  await mongoose.connect(process.env.MONGO_URI, {
    dbName: process.env.DB_NAME,
  });
  console.log("MongoDB Connected");

}

export default connectDB
```

---

# 10. Create Mongoose Model

```js
import mongoose from "mongoose";

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
});

export const User = mongoose.model("User", userSchema);
```

---

# 11. Generate JWT Token

```js
import jwt from "jsonwebtoken";

export function createToken(userId) {
  return jwt.sign({ id: userId }, process.env.JWT_SECRET, { expiresIn: "7d" });
}
```

---

# 12. Verify JWT Token

```js
import jwt from "jsonwebtoken";

export function verifyToken(req, res, next) {
  try {
    const token = req.headers.authorization?.split(" ")[1];
    req.user = jwt.verify(token, process.env.JWT_SECRET);
    next();
  } catch {
    res.status(403).send("Invalid token");
  }
}
```

---

# 13. Password Hashing (bcrypt)

```js
import bcrypt from "bcrypt";
const hashed = await bcrypt.hash("mypassword", 10);
```

---

# 14. File Upload With Multer

```js
import multer from "multer";

const upload = multer({ dest: "uploads/" });
       app.post("/upload", upload.single("file"), (req, res)=>{
  res.send("Uploaded")
 )};
```

---

# 15. Rate Limiting Middleware

```js
const rate = {};
export function rateLimit(req, res, next) {
  const ip = req.ip;
  rate[ip] = (rate[ip] || 0) + 1;
  if (rate[ip] > 50) return res.status(429).send("Too many requests");
  next();
}
```

---

# 16. CORS Setup

```js
import cors from "cors";
app.use(cors({ origin: "*" }));
```

---

# 17. React Fetch Hook

```jsx
export function useFetch(url) {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch(url)
      .then((r) => r.json())
      .then(setData);
  }, [url]);
  return data;
}
```

---

# 18. React Debounce Hook

```jsx
export function useDebounce(value, delay = 400) {
  const [v, setV] = useState(value);
  useEffect(() => {
    const t = setTimeout(() => setV(value), delay);
    return () => clearTimeout(t);
  }, [value]);
  return v;
}
```

---

# 19. React LocalStorage Hook

```jsx
export function useLocal(key, initial) {
  const [value, setValue] = useState(
    () => JSON.parse(localStorage.getItem(key)) || initial
  );
  useEffect(() => localStorage.setItem(key, JSON.stringify(value)), [value]);
  return [value, setValue];
}
```

---

# 20. React Protected Route

```jsx
export function Protected({ children }) {
  const logged = localStorage.getItem("auth");
  return logged ? children : <Navigate to="/login" />;
}
```

---

# 21. Scroll to Top (React Router)

```jsx
useEffect(() => {
  window.scrollTo(0, 0);
}, [location.pathname]);
```

---

# 22. Tailwind Modern Card

```html
<div class="p-5 max-w-sm bg-white rounded-xl shadow hover:shadow-lg transition">
  <img src="https://picsum.photos/400" class="rounded-lg" />
  <h2 class="mt-3 text-lg font-semibold">Modern UI</h2>
  <p class="text-gray-600">Reusable card template</p>
</div>
```

---

# 23. Reels Feed UI React Tailwindcss

````Reels Feed UI React Tailwindcss

```jsx

import { useState, useEffect, useRef } from 'react'

// Dummy video data
const VIDEOS = [
  {
    id: 1,
    username: '@foodlover',
    description: 'Best pasta recipe you will ever try! 🍝',
    likes: '234K',
    comments: '1.2K',
    shares: '890',
    videoUrl: '/delicious-pasta-dish-cooking.jpg',
  },
  {
    id: 2,
    username: '@travelbug',
    description: 'Hidden gem in Bali 🌴 #travel #paradise',
    likes: '567K',
    comments: '3.4K',
    shares: '2.1K',
    videoUrl: '/tropical-beach-paradise-sunset.jpg',
  },
  {
    id: 3,
    username: '@fitnessguru',
    description: '30-day transformation challenge 💪',
    likes: '892K',
    comments: '5.6K',
    shares: '4.3K',
    videoUrl: '/fitness-workout-gym-motivation.jpg',
  },
  {
    id: 4,
    username: '@petcorner',
    description: 'When your dog realizes it\'s bath time 😂🐕',
    likes: '1.2M',
    comments: '8.9K',
    shares: '6.7K',
    videoUrl: '/cute-funny-dog-playing.jpg',
  },
  {
    id: 5,
    username: '@techreview',
    description: 'Latest smartphone unboxing! Worth it? 📱',
    likes: '445K',
    comments: '2.8K',
    shares: '1.5K',
    videoUrl: '/modern-smartphone-technology-gadget.jpg',
  },
  {
    id: 6,
    username: '@artcreator',
    description: 'Time-lapse of my latest painting 🎨',
    likes: '678K',
    comments: '4.2K',
    shares: '3.1K',
    videoUrl: '/colorful-abstract-art.png',
  },
]

export default function ReelsFeed() {
  const [currentIndex, setCurrentIndex] = useState(0)
  const [isTransitioning, setIsTransitioning] = useState(false)
  const containerRef = useRef(null)
  const touchStartY = useRef(0)
  const touchEndY = useRef(0)

  // Navigate to next video
  const goToNext = () => {
    if (isTransitioning) return
    if (currentIndex < VIDEOS.length - 1) {
      setIsTransitioning(true)
      setCurrentIndex(currentIndex + 1)
      setTimeout(() => setIsTransitioning(false), 500)
    }
  }

  // Navigate to previous video
  const goToPrevious = () => {
    if (isTransitioning) return
    if (currentIndex > 0) {
      setIsTransitioning(true)
      setCurrentIndex(currentIndex - 1)
      setTimeout(() => setIsTransitioning(false), 500)
    }
  }

  // Handle mouse wheel scroll
  useEffect(() => {
    const handleWheel = (e) => {
      e.preventDefault()
      if (e.deltaY > 0) {
        goToNext()
      } else if (e.deltaY < 0) {
        goToPrevious()
      }
    }

    const container = containerRef.current
    if (container) {
      container.addEventListener('wheel', handleWheel, { passive: false })
    }

    return () => {
      if (container) {
        container.removeEventListener('wheel', handleWheel)
      }
    }
  }, [currentIndex, isTransitioning])

  // Handle touch swipe for mobile
  const handleTouchStart = (e) => {
    touchStartY.current = e.touches[0].clientY
  }

  const handleTouchMove = (e) => {
    touchEndY.current = e.touches[0].clientY
  }

  const handleTouchEnd = () => {
    const swipeDistance = touchStartY.current - touchEndY.current
    const minSwipeDistance = 50

    if (Math.abs(swipeDistance) > minSwipeDistance) {
      if (swipeDistance > 0) {
        goToNext()
      } else {
        goToPrevious()
      }
    }
  }

  // Handle keyboard navigation
  useEffect(() => {
    const handleKeyDown = (e) => {
      if (e.key === 'ArrowDown') {
        goToNext()
      } else if (e.key === 'ArrowUp') {
        goToPrevious()
      }
    }

    window.addEventListener('keydown', handleKeyDown)
    return () => window.removeEventListener('keydown', handleKeyDown)
  }, [currentIndex, isTransitioning])

  const currentVideo = VIDEOS[currentIndex]

  return (
    <div
      ref={containerRef}
      className="relative w-full h-screen overflow-hidden bg-black"
      onTouchStart={handleTouchStart}
      onTouchMove={handleTouchMove}
      onTouchEnd={handleTouchEnd}
    >
      {/* Video Container with Transition */}
      <div
        className="absolute inset-0 transition-transform duration-500 ease-out"
        style={{
          transform: `translateY(-${currentIndex * 100}vh)`,
        }}
      >
        {VIDEOS.map((video, index) => (
          <div
            key={video.id}
            className="relative w-full h-screen flex items-center justify-center"
          >
            {/* Video Background */}
            <img
              src={video.videoUrl || "/placeholder.svg"}
              alt={video.description}
              className="absolute inset-0 w-full h-full object-cover"
            />

            {/* Gradient Overlay */}
            <div className="absolute inset-0 bg-gradient from-black/20 via-transparent to-black/60" />

            {/* Video Info - Bottom Left */}
            <div className="absolute bottom-0 left-0 p-6 pb-24 max-w-md z-10">
              <h2 className="text-white font-bold text-lg mb-2">
                {video.username}
              </h2>
              <p className="text-white text-sm leading-relaxed mb-4">
                {video.description}
              </p>
            </div>

            {/* Action Buttons - Right Side */}
            <div className="absolute right-4 bottom-24 flex flex-col gap-6 z-10">
              {/* Like Button */}
              <button className="flex flex-col items-center gap-1 group">
                <div className="w-12 h-12 rounded-full bg-white/10 backdrop-blur-sm flex items-center justify-center transition-all group-hover:bg-white/20 group-active:scale-90">
                  <svg
                    className="w-7 h-7 text-white"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      strokeLinecap="round"
                      strokeLinejoin="round"
                      strokeWidth={2}
                      d="M4.318 6.318a4.5 4.5 0 000 6.364L12 20.364l7.682-7.682a4.5 4.5 0 00-6.364-6.364L12 7.636l-1.318-1.318a4.5 4.5 0 00-6.364 0z"
                    />
                  </svg>
                </div>
                <span className="text-white text-xs font-semibold">
                  {video.likes}
                </span>
              </button>

              {/* Comment Button */}
              <button className="flex flex-col items-center gap-1 group">
                <div className="w-12 h-12 rounded-full bg-white/10 backdrop-blur-sm flex items-center justify-center transition-all group-hover:bg-white/20 group-active:scale-90">
                  <svg
                    className="w-7 h-7 text-white"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      strokeLinecap="round"
                      strokeLinejoin="round"
                      strokeWidth={2}
                      d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"
                    />
                  </svg>
                </div>
                <span className="text-white text-xs font-semibold">
                  {video.comments}
                </span>
              </button>

              {/* Share Button */}
              <button className="flex flex-col items-center gap-1 group">
                <div className="w-12 h-12 rounded-full bg-white/10 backdrop-blur-sm flex items-center justify-center transition-all group-hover:bg-white/20 group-active:scale-90">
                  <svg
                    className="w-7 h-7 text-white"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                  >
                    <path
                      strokeLinecap="round"
                      strokeLinejoin="round"
                      strokeWidth={2}
                      d="M8.684 13.342C8.886 12.938 9 12.482 9 12c0-.482-.114-.938-.316-1.342m0 2.684a3 3 0 110-2.684m0 2.684l6.632 3.316m-6.632-6l6.632-3.316m0 0a3 3 0 105.367-2.684 3 3 0 00-5.367 2.684zm0 9.316a3 3 0 105.368 2.684 3 3 0 00-5.368-2.684z"
                    />
                  </svg>
                </div>
                <span className="text-white text-xs font-semibold">
                  {video.shares}
                </span>
              </button>
            </div>
          </div>
        ))}
      </div>

      {/* Navigation Arrows - Right Side */}
      <div className="absolute right-6 top-1/2 -translate-y-1/2 flex flex-col gap-4 z-20">
        {/* Up Arrow */}
        <button
          onClick={goToPrevious}
          disabled={currentIndex === 0}
          className="w-12 h-12 rounded-full bg-white/20 backdrop-blur-md flex items-center justify-center transition-all hover:bg-white/30 active:scale-90 disabled:opacity-30 disabled:cursor-not-allowed"
        >
          <svg
            className="w-6 h-6 text-white"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth={2.5}
              d="M5 15l7-7 7 7"
            />
          </svg>
        </button>

        {/* Down Arrow */}
        <button
          onClick={goToNext}
          disabled={currentIndex === VIDEOS.length - 1}
          className="w-12 h-12 rounded-full bg-white/20 backdrop-blur-md flex items-center justify-center transition-all hover:bg-white/30 active:scale-90 disabled:opacity-30 disabled:cursor-not-allowed"
        >
          <svg
            className="w-6 h-6 text-white"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
          >
            <path
              strokeLinecap="round"
              strokeLinejoin="round"
              strokeWidth={2.5}
              d="M19 9l-7 7-7-7"
            />
          </svg>
        </button>
      </div>

      {/* Progress Indicator */}
      <div className="absolute top-6 left-1/2 -translate-x-1/2 flex gap-1 z-20">
        {VIDEOS.map((_, index) => (
          <div
            key={index}
            className={`h-1 rounded-full transition-all duration-300 ${
              index === currentIndex
                ? 'w-8 bg-white'
                : 'w-1 bg-white/40'
            }`}
          />
        ))}
      </div>

      {/* Swipe Hint for Mobile */}
      <div className="absolute bottom-8 left-1/2 -translate-x-1/2 text-white/60 text-xs z-20 md:hidden">
        Swipe up or down
      </div>
    </div>
  )
}
````

---

# 24. CSS Glassmorphism

```css
.glass {
  backdrop-filter: blur(14px);
  background: rgba(255, 255, 255, 0.15);
  border-radius: 16px;
}
```

---

# 25. LocalStorage With Expiry

```js
function setExp(key, value, minutes) {
  const item = { value, expiry: Date.now() + minutes * 60000 };
  localStorage.setItem(key, JSON.stringify(item));
}
function getExp(key) {
  const item = JSON.parse(localStorage.getItem(key));
  if (!item || Date.now() > item.expiry) return null;
  return item.value;
}
```

---

# 26. Generate Unique IDs

```js
const id = crypto.randomUUID();
```

---

# 27. Validate Email

```js
/^\S+@\S+\.\S+$/.test("user@mail.com");
```

---

# 28. Download File URL

```js
function download(url) {
  const a = document.createElement("a");
  a.href = url;
  a.download = url.split("/").pop();
  a.click();
}
```

---

# 29. Throttle Function

```js
function throttle(fn, limit) {
  let wait = false;
  return (...args) => {
    if (!wait) {
      fn(...args);
      wait = true;
      setTimeout(() => (wait = false), limit);
    }
  };
}
```

---

# 30. Debounce Function

```js
function debounce(fn, delay) {
  let t;
  return (...args) => {
    clearTimeout(t);
    t = setTimeout(() => fn(...args), delay);
  };
}
```
# 31. Custom Scroll bar Css
```css
<style>
      ::-webkit-scrollbar {
  width: 10px;
}

/* Track */
::-webkit-scrollbar-track {
  background: transparent;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #F97316;
  border-radius: 20px;
  cursor: pointer;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #f97416a1;
}
    </style>
```

# 32 Cloudinary Uploader Setup
A. Cloudinary config (cloudinary.js)
```js
import { v2 as cloudinary } from "cloudinary";

cloudinary.config({
  cloud_name: process.env.CLOUD_NAME,
  api_key: process.env.CLOUD_API_KEY,
  api_secret: process.env.CLOUD_API_SECRET,
});

export default cloudinary;
```
B. Multer setup (multer.js)
```js
import multer from "multer";

const storage = multer.memoryStorage();

const upload = multer({ storage });

export default upload;

```
C. Upload route (uploadRoute.js)
```js
import express from "express";
import upload from "./multer.js";
import cloudinary from "./cloudinary.js";

const router = express.Router();

router.post("/upload", upload.single("image"), async (req, res) => {
  try {
    if (!req.file) {
      return res.status(400).json({ message: "No file received" });
    }

    const result = await cloudinary.uploader.upload_stream(
      { folder: "myUploads" },
      (error, uploadResult) => {
        if (error) {
          console.log(error);
          return res.status(500).json({ message: "Cloudinary upload failed" });
        }

        return res.status(200).json({
          url: uploadResult.secure_url,
          public_id: uploadResult.public_id,
        });
      }
    );

    // Send buffer to Cloudinary
    result.end(req.file.buffer);

  } catch (err) {
    console.log(err);
    res.status(500).json({ message: "Server error" });
  }
});

export default router;

```
React Example
```js
const handleUpload = async (e) => {
  const file = e.target.files[0];
  const formData = new FormData();
  formData.append("image", file);

  const res = await fetch("http://localhost:5000/api/upload", {
    method: "POST",
    body: formData,
  });

  const data = await res.json();
  console.log("Uploaded Image URL:", data.url);
};

```
File input
```html
<input type="file" onChange={handleUpload} />
```
33 Request Logger
```js
const requestLogger = (req, res, next) => {
  console.log(`[${req.method}] ${req.originalUrl}`);
  next();
};

module.exports = requestLogger;

```
---






