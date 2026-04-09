# HTTP Headers

They are metadata about the original request and are used for content negotiation, validation, and authorization. It's like an address on the envelope in real life postal system.

## Why we need Headers?

Hamein inki zaroorat isliye hoti hai kyunke inke baghair server ko ye nahi pata chalega ke:

1. Aap kis format mein data chahte hain (JSON ya HTML?).

2. Kya aap login hain (Authentication)?

3. Kya data ko cache mein save karna hai ya har baar naya mangwana hai?

## Request Headers

**`Host`:** Batata hai ke request kis domain (e.g., `google.com`) ko ja rahi hai.

**`User-Agent`:** Browser ki maloomat (e.g., Chrome ya Firefox) taake server uske mutabiq content bhej sake.

**`Authorization`:** Sab se aham! Is mein JWT tokens ya API keys jati hain taake server ko pata chale aap authorized hain.

**`Accept`:** Batata hai ke client ko kis tarah ka data chahiye (e.g., `application/json`).

**`Content-Type`:** (POST/PUT mein) Batata hai ke jo data aap bhej rahe hain wo kis format mein hai.

## Response Headers

**`Content-Type`:** Batata hai ke server ne jo bheja hai wo image hai, HTML hai, ya JSON.

**`Cache-Control`:** Browser ko batata hai ke ye file kitni der tak save rakhni hai taake agli baar request fast ho.

**`Set-Cookie`:** Server iske zariye browser mein cookie save karwata hai (Session management ke liye).

## CORS Headers

### Access-Control-Allow-Origin

**Purpose:** Server batata hai ke kaunsi website (origin) cross-origin requests kar sakti hai.

**How it works:**

- Client apni origin automatically `Origin` header mein bhejta hai
- Server check karta hai aur response mein batata hai ke ye origin allowed hai ya nahi
- Agar server ye header na bhejye ya origin match na ho, to browser request block kar deta hai aur CORS error throw karta hai

**Client Request:**

```http
GET /api/data HTTP/1.1
Host: api.example.com
Origin: https://myapp.com
```

**Server Response:**

```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: https://myapp.com
Content-Type: application/json

{"data": "value"}
```

Ya phir sabhi origins ke liye:

```http
Access-Control-Allow-Origin: *
```

That mean any origin is allowed for CORS.

### 2. Access-Control-Allow-Methods

**Purpose:** Server batata hai ke kaun se HTTP methods (GET, POST, PUT, DELETE, etc.) allowed hain cross-origin requests ke liye.

**How it works:**

- Client preflight request (OPTIONS) mein `Access-Control-Request-Method` header bhejta hai
- Server response mein `Access-Control-Allow-Methods` se batata hai kaunse methods allowed hain

**Client Preflight Request:**

```http
OPTIONS /api/resource HTTP/1.1
Host: api.example.com
Origin: https://myapp.com
Access-Control-Request-Method: POST
```

**Server Response:**

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://myapp.com
Access-Control-Allow-Methods: GET, POST, PUT, DELETE
Access-Control-Max-Age: 86400
```

### Access-Control-Allow-Headers

**Purpose:** Server batata hai ke kaunse custom headers ko support karta hai cross-origin requests mein.

**How it works:**

- Client preflight request mein `Access-Control-Request-Headers` bhejta hai (jisme wo headers hote hain jo client use karna chahta hai)
- Server response mein `Access-Control-Allow-Headers` se batata hai kaunse headers allowed hain
- Agar requested header allowed nahi hai, to browser actual request block kar deta hai

**Client Preflight Request:**

```http
OPTIONS /api/resource HTTP/1.1
Host: api.example.com
Origin: https://myapp.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Authorization, X-Custom-Header
```

**Server Response:**

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://myapp.com
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: Authorization, X-Custom-Header
Access-Control-Max-Age: 86400
```

### 4. Access-Control-Max-Age

**Purpose:** Server batata hai ke preflight request ka response kitni der tak cache mein store rahega (seconds mein).

**How it works:**

- Har cross-origin request se pehle preflight request bhejni bahut costly hoti hai (extra network round trip)
- `Access-Control-Max-Age` se browser preflight response ko cache kar leta hai
- Cache validity period ke andar same type ki requests ke liye dobara preflight nahi bheji jati
- Isse performance improve hoti hai

**Client Preflight Request:**

```http
OPTIONS /api/resource HTTP/1.1
Host: api.example.com
Origin: https://myapp.com
Access-Control-Request-Method: POST
Access-Control-Request-Headers: Authorization, Content-Type
```

**Server Response:**

```http
HTTP/1.1 204 No Content
Access-Control-Allow-Origin: https://myapp.com
Access-Control-Allow-Methods: GET, POST, PUT
Access-Control-Allow-Headers: Authorization, Content-Type
Access-Control-Max-Age: 86400
```

**Explanation:**

- `Access-Control-Max-Age: 86400` ka matlab hai ke browser is preflight response ko **24 hours (86400 seconds)** tak cache mein rakhega
- Agli 24 hours tak, agar same origin se same method aur same headers ke sath request aayi, to browser **preflight skip kar dega** aur seedha actual request bhej dega
- Cache expire hone ke baad dobara preflight request hogi

**Benefits:**

- Network requests kam hoti hain
- API calls faster ho jati hain
- Server load reduce hota hai

**Common Values:**

- `86400` = 24 hours (common default)
- `3600` = 1 hour
- `600` = 10 minutes
- `-1` = caching disable (har baar preflight)
