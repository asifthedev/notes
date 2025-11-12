# CORS

It stands for Cross Origin Resource Sharing.  It’s a **browser security feature** that controls which websites can send requests to your server

## What is an "Origin"?

An origin is made up of:

```
protocol + domain + port
```

### Example — Why It Exists

Let’s say your **frontend** runs at:

```
http://127.0.0.1:5500
```

and your **Express backend** runs at:

```
http://localhost:5000
```

When your frontend JavaScript tries to do:

```js
fetch("http://localhost:5000/api/data")
```

the browser says:

> ❌ “Blocked by CORS policy!”

because **5500 ≠ 5000** → that’s a *different origin*.

## How to Fix CORS in Express (Easy Way)

### Step 1. Install CORS package

```bash
npm install cors
```

### Step 2. Import and use in your `server.js`

```js
import express from "express";
import cors from "cors";

const app = express();

// ✅ Allow requests from frontend origin
app.use(
  cors({
    origin: "http://127.0.0.1:5500", // your frontend address
    methods: ["GET", "POST", "PUT", "DELETE"],
    credentials: true, // if using cookies or auth headers
  })
);
```

That’s it. 🎉 Now the browser allows your frontend to call your backend.

---

## ⚙️ Production Setup (Recommended)

When you deploy, allow only your **frontend domain** (never use `*` in production).

```js
const allowedOrigins = ["https://yourfrontend.com", "https://admin.yourfrontend.com"];

app.use(
  cors({
    origin: function (origin, callback) {
      if (!origin || allowedOrigins.includes(origin)) {
        callback(null, true);
      } else {
        callback(new Error("Not allowed by CORS"));
      }
    },
  })
);
```

---

## 🔍 Bonus — Manual Headers (if you don’t want `cors` package)

You can set headers manually too:

```js
app.use((req, res, next) => {
  res.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization");
  next();
});
```

---

## 💡 TL;DR Summary

| Term                 | Meaning                                               |
| -------------------- | ----------------------------------------------------- |
| **CORS**             | Browser rule that blocks unsafe cross-origin requests |
| **Fix**              | Tell the server which origins are allowed             |
| **Express Solution** | Use the `cors` middleware                             |
| **Development Tip**  | Use `*` for local testing only                        |
| **Production Tip**   | Always whitelist only your frontend domain            |

---

Would you like me to show a **small working Express server + HTML frontend example** that demonstrates the CORS error and its fix? It helps you *see* what happens in real time.
