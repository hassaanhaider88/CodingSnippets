Here’s a clean, ready-to-paste **README.md** you can use in your GitHub repo.
I kept it simple, helpful and friendly, with **10 practical web-development code snippets** (frontend + backend) and a **modern UI look** using emojis, clean headings, spacing, and code formatting.

If you want more snippets or want to expand into categories, just tell me.

---

# 🚀 Web Development Code Snippets Library

A free collection of useful **basic to advanced** code snippets for web developers.
Copy → Paste → Use. No credit needed.

---

## 📂 Table of Contents

1. Smooth Scroll to Section
2. Debounce Function
3. Throttle Function
4. Copy to Clipboard
5. Detect Dark Mode
6. Axios GET Request
7. Express Basic Server
8. MongoDB Connection
9. React Fetch Hook
10. Tailwind Responsive Card UI

---

## 1️⃣ Smooth Scroll to Section (JavaScript)

```js
document.querySelectorAll("[data-scroll]").forEach(btn => {
  btn.addEventListener("click", () => {
    const target = document.querySelector(btn.dataset.scroll);
    target.scrollIntoView({ behavior: "smooth" });
  });
});
```

---

## 2️⃣ Debounce Function (JavaScript)

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

## 3️⃣ Throttle Function (JavaScript)

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

## 4️⃣ Copy to Clipboard (JavaScript)

```js
function copy(text) {
  navigator.clipboard.writeText(text).then(() => {
    console.log("Copied!");
  });
}
```

---

## 5️⃣ Detect Dark Mode (JavaScript)

```js
const isDark = window.matchMedia("(prefers-color-scheme: dark)").matches;
console.log(isDark ? "Dark Mode" : "Light Mode");
```

---

## 6️⃣ Axios GET Request (Frontend or Backend)

```js
import axios from "axios";

async function getData() {
  const res = await axios.get("https://api.example.com/data");
  console.log(res.data);
}
```

---

## 7️⃣ Basic Express Server (Node.js)

```js
import express from "express";
const app = express();

app.get("/", (req, res) => {
  res.send("Hello Developer!");
});

app.listen(3000, () => console.log("Server running on 3000"));
```

---

## 8️⃣ MongoDB Connection (Mongoose)

```js
import mongoose from "mongoose";

mongoose.connect(process.env.MONGO_URI)
  .then(() => console.log("DB Connected"))
  .catch(err => console.error(err));
```

---

## 9️⃣ React Hook for Fetching Data

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

## 🔟 Tailwind Modern UI Card Component

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

## ⭐ Contribute

Got a helpful snippet? Add it through a pull request and help other developers learn faster.

---

## ❤️ Support

If you like this repo, give it a ⭐ on GitHub. It motivates me to add more snippets!

---

If you want, I can also create:

✅ A Logo
✅ Folder structure
✅ More snippets (React, Node, Auth, Tailwind, MongoDB, API helpers)
✅ A landing page UI for your repo

Just tell me.
