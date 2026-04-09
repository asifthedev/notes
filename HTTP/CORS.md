### CORS

In order to understand CORS we have to first understand some prequsit concepts then can only understanding CORS and their importance makes more sense.



## What is an Origin?

Origin 3 cheezo say mill kar banti hey, ager in mey say kisi aik bhi changer kar diya to yeah aik different origin ban jaye gi

```
protocol + domain + port
```

**Protocol**

Ye wo tareeqa hai jis se data transfer hota hai (e.g., `http` ya `https`).

**Domain**

Ye website ka naam hota hai (e.g., `google.com` ya `localhost`).

**Port**

Ye wo rasta (channel) hota hai jis par server listen kar raha hota hai. Default mein `http` ke liye port **80** aur `https` ke liye **443** hota hai, lekin development mein ye `3000` ya `5000` bhi ho sakta hai.

**Example**

```mongodb
http://localhost:3000/
https://localhost:3000/
```

These are two different origins, Heyn? Yes, becuase the **protocol** http ≠ https.

## Same Origin Policy

By default browser same origin policy follows karta hey, yani browser server ko request sirf same origin say allowed karta hey.

Iska matlab hai ke `website-a.com` sirf `website-a.com` ke hi resources ko hi access kar sakti hai. Agar `website-a.com` `api-b.com` se data mangna chahe, to browser security ki wajah se usay rok dega, jab tak ke `api-b.com` khud allow na karey na de.

## Voilation of Same Origin Policy

If the client and the server are on different origins, this violates the browser’s default same-origin policy. In that case, the server must explicitly allow the client through CORS; otherwise, the browser will block requests to the server from a different origin.

Let see an example that voilates the browser same origin policy:-

Let’s say your **frontend** runs at:

```
http://localhost:5500
```

and your **Express backend** runs at:

```
http://localhost:5000
```

**NOTE:** The frontend and backend are both running on different **PORT**.

When your frontend JavaScript tries to do:

```js
fetch("http://localhost:5000/api/data")
```

The browser says:

> “Blocked by CORS policy!”

because the port **5500 ≠ 5000** → that’s a *different origin*.

## CORS

It stands for Cross-Origin Resource Sharing. Yani app apney server k resrouces ko aik esay client ko allow kar rahey heyn Jiska origin apke server k origin say different hey.

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

That’s it. Now the browser allows your frontend to call your backend.

## Production Setup (Recommended)

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

### Bonus — Manual Headers (if you don’t want `cors` package)

You can set headers manually too:

```js
app.use((req, res, next) => {
  res.setHeader("Access-Control-Allow-Origin", "http://127.0.0.1:5500");
  res.setHeader("Access-Control-Allow-Methods", "GET, POST, PUT, DELETE, OPTIONS");
  res.setHeader("Access-Control-Allow-Headers", "Content-Type, Authorization");
  next();
});
```
