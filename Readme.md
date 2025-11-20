# Code Snippets

A free collection of useful **basic to advanced** code snippets for Programmers 🐱‍👤.
Copy → Paste → Use. .

---
## 📂 Table of Contents

1. [Smooth Scroll to Section](#1️⃣-smooth-scroll-to-section-javascript)
2. [Debounce Function](#2️⃣-debounce-function-javascript)
3. [Throttle Function](#3️⃣-throttle-function-javascript)
4. [Copy to Clipboard](#4️⃣-copy-to-clipboard-javascript)
5. [Detect Dark Mode](#5️⃣-detect-dark-mode-javascript)
6. [Axios GET Request](#6️⃣-axios-get-request-frontend-or-backend)
7. [Express Basic Server](#7️⃣-basic-express-server-nodejs)
8. [MongoDB Connection](#8️⃣-mongodb-connection-mongoose)
9. [React Fetch Hook](#9️⃣-react-hook-for-fetching-data)
10. [Tailwind Responsive Card UI](#🔟-tailwind-modern-ui-card-component)
11. [Reels Feed UI (React + Tailwind)](#1️⃣1️⃣-tiktokinstayt-shorts-like-reels-ui-react--tailwindcss)

---

# 1. Smooth Scroll to Section (JavaScript)

```js
document.querySelectorAll("[data-scroll]").forEach(btn => {
  btn.addEventListener("click", () => {
    const target = document.querySelector(btn.dataset.scroll);
    target.scrollIntoView({ behavior: "smooth" });
  });
});
```

---

# 2. Debounce Function (JavaScript)

```js
function debounce(fn, delay) {
  let timeout;
  return (...args) => {
    clearTimeout(timeout);
    timeout = setTimeout(() => fn(...args), delay);
  };
}
```

---

# 3. Throttle Function (JavaScript)

```js
function throttle(fn, limit) {
  let waiting = false;
  return (...args) => {
    if (!waiting) {
      fn(...args);
      waiting = true;
      setTimeout(() => (waiting = false), limit);
    }
  };
}
```

---

# 4. Copy to Clipboard (JavaScript)

```js
function copy(text) {
  navigator.clipboard.writeText(text).then(() => {
    console.log("Copied!");
  });
}
```

---

# 5. Detect Dark Mode (JavaScript)

```js
const isDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
console.log(isDark ? "Dark Mode" : "Light Mode");
```

---

# 6. Axios GET Request (Frontend or Backend)

```js
import axios from "axios";

async function getData() {
  const res = await axios.get("https://api.example.com/data");
  console.log(res.data);
}
```

---

# 7. Basic Express Server (Node.js)

```js
import express from "express";
const app = express();

app.get("/", (req, res) => {
  res.send("Hello Developer!");
});

app.listen(3000, () => console.log("Server running on 3000"));
```

---

# 8. MongoDB Connection (Mongoose)

```js
import mongoose from "mongoose";

mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log("DB Connected"))
  .catch(err => console.error(err));
```

---

# 9. React Hook for Fetching Data

```js
import { useEffect, useState } from "react";

export function useFetch(url) {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(setData);
  }, [url]);

  return data;
}
```

---

# 10. Tailwind Modern UI Card Component

```html
<div class="max-w-sm rounded-xl shadow-lg p-5 bg-white hover:shadow-xl transition">
  <img src="https://picsum.photos/400" class="rounded-lg mb-3" />
  <h2 class="text-xl font-semibold">Modern UI Card</h2>
  <p class="text-gray-600 mt-1">A clean reusable card template.</p>
  <button class="mt-4 bg-black text-white px-4 py-2 rounded-lg">
    Explore
  </button>
</div>
```

---

# 11. TikTok/Insta/YT Shorts Like Reels UI React + Tailwindcss
```jsx
'use client'

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
            <div className="absolute inset-0 bg-gradient-to-b from-black/20 via-transparent to-black/60" />

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
```
---


## ⭐ Contribute

Got a helpful snippet? Add it through a pull request and help other developers learn faster.

---

## ❤️ Support

If you like this repo, give it a ⭐ on GitHub. It motivates me to add more snippets!

---


