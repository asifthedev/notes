# HTTP Module

It's used to create `http` server.

## Create an HTTP Server

```js
import http from "http";

const server = http.createServer((req, res) => {
});
```

## Port and Host Binding

```js
import http from "http";

const server = http.createServer((req, res) => {
});

// binding server
server.listen(3000, 'localhost', () => {
    console.log("Server is started!");
})
```

## Request Object

The request object contains information about incoming HTTP request. For example:-

```js
const server = http.createServer((req, res) => {
  console.log(req.method);      // HTTP method (GET, POST, etc.)
  console.log(req.url);          // Requested URL
  console.log(req.headers);      // Request headers
  console.log(req.httpVersion);  // HTTP version
});
```

`req.url` - woh end point jisay request ayi hey

`req.method` - HTTP method jo request kelye use huwa hey

`req.headers` - client ney jo headers request mey send kiye heyn

## How to read body of the `http` message?

```js
if (req.url === "/register" && req.method === "POST") {
    
    let body = "";
    req.on("data", (chunk) => {
      body += chunk;
    });

    req.on("end", () => {
      try {
        const data = Buffer.from(body).toString("utf-8");
        console.log(data);
      } catch (err) {
        console.log(err);
      }
    });

    res.writeHead(200, "OK");
    res.end(JSON.stringify({ success: true }));
  }
```

Axha g esa hey k data hamey chunks mey milta hey buffer k chunks, jab data k stream ani shuru hoti hey to `data` name ka event emit hota hey, to ham `req.on()` method ki mdad say is event ko handle kartey heyn.

Mujeh lagta hey har data chunk k aney pay `data` event emit hota hey or ham usay kis string mey jodtay rehtay as in the given code snippet

 Ham aney waley chunks ko ya to aik array mey push  `chunks.push(chunks)` kar saktey heyn jo baad mey  `Buffer.concat(arrayChunks)` k zariyay say aik buffer array ban jaye ga.

Jab sarey chunks poray a jatey heyn to `end` event emit hota hey yani sara data receive  ho giya hey or abh ham isay use kar saktey heyn.

## Response Object

### Key Properties

`res.statusCode`

Sets the HTTP status code for the response that helps client understand what happened with the request:

```js
res.statusCode = 200
```

`res.statusMessage`

Sets the status message (optional, as there are defaults):

```js
res.statusMessage = 'OK'
```

### Essential Methods

`res.setHeader(name, value)`

It's used to set single header at a time:

```js
res.setHeader('Content-Type', 'text/plain')
```

You can even overwirte the same header later:

```js
res.setHeader('Content-Type', 'application/json')
```

`res.writeHead(statusCode, statusMessage, {headers})`

It helps you write header:

- But once you call the `writeHead()` you can't write the headers again 
  
  ```js
  res.writeHead(200, "OK", { "content-type": "text/plain" });
  res.setHeader("Content-Type", "application/json");
  res.end("Hello, from the server!");
  ```

- ```js
  > Error: Cannot set headers after they are sent to the client
  ```

- You can also set multiple headers at the same time in headers object

- ```js
  res.writeHead(200, "OK", {
      "content-type": "text/plain",        
      "accept-encoding": "utf8",
  })
  ```

#### res.write()

Used to write the response body, sends a chunk of the response body. Can be called multiple times:

```js
res.write("Hello ");
res.write("World");
res.end();
```

The body client recieved:

```js
Hello World
```

#### res.end()

Yeah btata hey k response k sarey headers or body send ho gayi hey

```js
res.end('Done!'); // Send data and end

// Or just end without data
res.end();
```

> **Always call `res.end()`**: Every response must end with `res.end()`, otherwise the connection will hang.

**Key Points:**

- Must be called on every response, or the connection will hang
- Can optionally send data as the final chunk
- After calling `end()`, you cannot write more data
- The connection is closed after `end()` is called


