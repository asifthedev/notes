# Fetch API in JavaScript

Yeah aik function hey jo http network request k zariye say server say data ko fetch karney kelye istimal hota hey. Yeah modern alernative hey purani XMLHttpRequest (XHR) ka. 

## Argumetns

Fethc do arugemtns as input layta hey 

```log
fetch(url, options)
```

## Return Type

Fethc hamesha aik promise return karta hey jo k fullfilled honey per aik `Response` object ouput k tor per deyta hey.

## HTTP Errors

Fetch tabhi error deyta hey jab request succfull ho he na, jesay k network issue ki waja say. HTTP Errors jesa 404 (Not Found) pay koee error nahi ata woh apko khud hi status code k help logic likhna parta hey. 

## Options Argument in Fetch

## 1. **method**

Defines the HTTP method.

```js
fetch("https://reqres.in/api/users", {
  method: "POST" // GET, POST, PUT, DELETE, PATCH, etc.
});
```

Default = `"GET"`

## 2. **headers**

Used to send metadata like content type, authentication tokens, etc.

```js
fetch("https://reqres.in/api/users", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Authorization": "Bearer token_here"
  }
});
```

## 3. **body**

Used to send data (with `POST`, `PUT`, `PATCH`).

```js
fetch("https://reqres.in/api/users", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({
    name: "Asif",
    job: "Web Developer"
  })
});
```

⚠️ `body` is **ignored** in GET and HEAD requests.

## 4. **mode**

Controls **CORS** (Cross-Origin Resource Sharing).

```js
fetch("https://example.com/api", {
  mode: "cors"       // default, allows cross-origin if server permits
  // mode: "same-origin"  // only if same domain
  // mode: "no-cors"      // opaque response, limited access
});
```

## 5. **credentials**

Manages cookies and authentication.

```js
fetch("https://example.com/data", {
  credentials: "include" // always send cookies (even cross-origin)
  // credentials: "same-origin" // default, send cookies if same domain
  // credentials: "omit"        // never send cookies
});
```

## 6. **cache**

Controls caching behavior.

```js
fetch("https://example.com/data", {
  cache: "default"        // normal HTTP cache rules
  // "no-store"           // always fetch fresh
  // "reload"             // always reload from server
  // "no-cache"           // validate with server before using cache
  // "force-cache"        // use cache if available, else fetch
  // "only-if-cached"     // only use cache (errors if not available)
});
```

## 7. **redirect**

How redirects should be handled.

```js
fetch("https://example.com", {
  redirect: "follow" // default, automatically follow redirects
  // "manual"        // caller handles redirects
  // "error"         // throw error on redirect
});
```

## 8. **referrer & referrerPolicy**

Controls what gets sent as the HTTP `Referer` header.

```js
fetch("https://example.com", {
  referrer: "https://mysite.com", 
  referrerPolicy: "no-referrer" // don’t send referrer info
  // other values: "origin", "same-origin", "strict-origin", etc.
});
```

## 9. **integrity**

Used with **Subresource Integrity (SRI)** to ensure the resource hasn’t been tampered with.

```js
fetch("https://cdn.example.com/script.js", {
  integrity: "sha256-abcdef123456..."
});
```

## 10. **signal**

Abort ongoing requests.

```js
let controller = new AbortController();

fetch("https://example.com/data", {
  signal: controller.signal
});

// cancel request later
controller.abort();
```

# Quick Summary of Important Options

- `method` → GET, POST, PUT, DELETE, etc.

- `headers` → send extra info (auth, content-type)

- `body` → send data (with POST/PUT)

- `mode` → CORS control

- `credentials` → cookies & auth

- `cache` → caching rules

- `redirect` → handle redirects

- `referrer` / `referrerPolicy` → control referrer header

- `integrity` → SRI checks

- `signal` → cancel request

# Response Object

A **Response object** represents the HTTP response returned by `fetch()`.

- It contains:
  
  - Metadata (status code, headers, ok/not ok, etc.)
  
  - Methods to read the body (JSON, text, blob, etc.)

# Basic Example

```js
async function getData() {
  let response = await fetch("https://reqres.in/api/users?page=2");

  console.log(response.status); // 200
  console.log(response.ok);     // true
  console.log(response.headers.get("content-type")); // "application/json; charset=utf-8"

  let data = await response.json();
  console.log(data);
}

getData();
```

# Response Properties

### 1. **status**

HTTP status code

```js
console.log(response.status); // e.g., 200, 404, 500
```

# 

### 2. **ok**

Boolean → `true` if status is **200–299**

```js
if (!response.ok) {
  throw new Error("Something went wrong");
}
```

### 3. **statusText**

Text message from server (not always reliable).

```js
console.log(response.statusText); // e.g., "OK", "Not Found"
```

### 4. **url**

The final URL (after redirects).

```js
console.log(response.url);
```

### 5. **headers**

All response headers (case-insensitive).

```js
console.log(response.headers.get("content-type"));
```

# Response Body Methods

Important: These can be called **only once** (because response body is a stream).

- **response.json()** → parses JSON into object

```js
let data = await response.json();
```

- **response.text()** → reads as string

```js
let text = await response.text();
```

- **response.blob()** → reads as file/blob (useful for images, PDFs)

```js
let img = await response.blob();
```

- **response.arrayBuffer()** → binary data

```js
let buffer = await response.arrayBuffer();
```

- **response.formData()** → converts to FormData object

```js
let form = await response.formData();
```

# Example: Handling Errors

```js
async function fetchUser() {
  let response = await fetch("https://reqres.in/api/users/23"); // non-existing

  if (!response.ok) {
    console.log(`Error: ${response.status} ${response.statusText}`);
    return;
  }

  let data = await response.json();
  console.log(data);
}

fetchUser();
```

# Response Flow (Visual)

```
fetch() → Promise → Response object
         ↳ response.ok, response.status, response.headers
         ↳ response.json() / response.text() / response.blob() ...
```
