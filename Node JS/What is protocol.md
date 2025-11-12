## What is protocol?

A set of rules to regulate any kind of operation.

### What is Communication Protocol?

A set of rules that define how devices shall communicate with each other on the network.

## HTTP

It's stands for Hypertext Transfer Protocol. Yeah aik communication protocol hey jo **client (browser)** aur **server** ke darmiyan data exchange karne ke liye use hota hai.

## Statless Protocol

HTTP aik stateless protocol hey, har request aik independent request hoti hey. 

Aik dafa jab HTTP server client ko serve kar deyta hey to woh next time pixhli request ka context bhool jata hey.

Is wajah se agar user login kare to next request me server bhool jata hai ke yeh wahi user hai ya koi naya.

**Isi problem ko solve karne ke liye hum use karte hain:**

1. Cookies

2. Sessions

3. Tokens

### Cookies

Cookies are **small pieces of data stored on the client’s browser**, usually sent by the server. They help remember information like login status, preferences, or session IDs.

### Sessions

A **session** stores user data on the **server side** and assigns a **session ID** to the client (often stored in a cookie). It helps the server remember the user between requests.

### Tokens

Tokens (like **JWT – JSON Web Token**) are **encrypted strings** used to verify a user’s identity. The server gives a token after login, and the client sends it with each request to prove who they are. Commonly used in **stateless authentication** (like APIs).

---

## Web Clients and Servers

Web content lives on web servers. Web servers speak the HTTP protocol, so they are often called HTTP servers. The clients send HTTP requests to servers, and servers return the requested data in HTTP responses.

You probably use HTTP clients every day. The most common client is a web browser, such as Microsoft Internet Explorer or Google Chrome Web browsers request HTTP objects from servers and display the objects on your screen.

## Resources

Web servers host web resources. A web resource is the source of web content. The simplest kind of web resource is a static file on the web server’s filesystem, for example text files, HTML files, Microsoft Word etc.

However, resources don’t have to be static files. Resources can also be software pro grams (SAAS) that generate content on demand, like Google Drive, Figma etc.

## MIME Type

Har tranport honey waley object/resource ko aik text label say tag kar diya jata hey. Yeah text label yeah btata hey k HTTP request ya response mey kis kisam ka data transport ho raha hey. 

<img title="" src="file:///C:/Users/mrasi/AppData/Roaming/marktext/images/2025-10-16-08-20-33-image.png" alt="" width="499" data-align="center">

Web servers attach a MIME type to all HTTP object data. When a web browser gets an object back from a server, it looks at the associated MIME type to see if it knows how to handle the object.

```http
Content-type: image/jpeg
Content-length: 12984
```

A MIME type is a textual label, represented as a primary object type and a specific
 subtype, separated by a slash. For example:
 • An HTML-formatted text document would be labeled with type **text/html.**
 • A plain ASCII text document would be labeled with type **text/plain.**
 • A JPEG version of an image would be **image/jpeg.**
 • A GIF-format image would be **image/gif**

#### MIME Type For JSON

For **JSON**, the correct **MIME type** is: **`application/json`**

- `application` → means it’s **application data**, not plain text or image.

- `json` → means the format is **JavaScript Object Notation**.

```http
Content-type: application/json
```

## URL

It's used to uniquely identify any web resource on the internet/web server.  It stands for **Uniform Resource Locator**. It has three parts:-

### URL Syntax

Most URL schemes base their URL syntax on this nine-part general format:

`<scheme>://<user>:<password>@<host>:<port>/<path>;<params>?<query>#<frag>`

#### Scheme

Which protocol to use when accessing a server to get a resource.

```js
https://
```

#### Hosts and Ports

To find a resource on the Internet, an application needs to know what machine is
 hosting the resource and where on that machine it can find application or process on the server machine that has access to the desired resource.

Host server ka pata btata hey or port batati hey k server pay konsi application ya process ko request deyni jo handle karey ga qn server bhi aik app hey or it might possible server machine can be hosting multiple services like your database etc.

> Hostname and port are separated by `:` colon

```url
https://example.com:80
```

- `example.com` -> hostname

- `80` port name

#### Username & Password

More interesting components are the user and password components. Many servers require a username and password before you can access data through them.

```url
mongodb://asifUser:fakePass123@localhost:27017/sampleDB
```

**Explaination:**

`mongodb://` → MongoDB protocol

`asifUser` → username

`fakePass123` → password

#### Path

The path component of the URL specifies where on the server machine the resource
 lives.

```js
http://www.joes-hardware.com:80/seasonal/index-fall.html
```

The path in this URL is `/seasonal/index-fall.html`, which resembles a filesystem path on a Unix filesystem. The path is the information that the server needs to locate the resource.

#### Parameters

After this you pass the parameter using the given syntax

```js
https://example.com/path;key1=value1&key2=value2
```

#### Query String

It helps you specify or narrow down your result or resouce you asking for. It's sepratd by the `?` symbol from other part of the URL.

```js
http://www.joes-hardware.com/inventory-check.cgi?item=12731&color=blue
```

#### Fragment

Kisi resource k specific part ko refer karney kelye use hota hey jesay hamey kisi html page k specfic section ko refer karney kelye. isay `#` symbol k sath seprate kia jata hey

```js
https://asifshahzad.me/home/#testimonials 
```

## Transaction

An HTTP transaction consists of a request command (sent from client to server), and a response result (sent from the server back to the client). This communication happens with formatted blocks of data called HTTP messages

## Methods

HTTP methods server ko batatey heyn k request k sath kia karna hey, The HTTP specifications have defined a set of common request methods.

| Method | Command Description                                                                                                  |
| ------ | -------------------------------------------------------------------------------------------------------------------- |
| GET    | Get ka mtlb hey k `named resource` ko server say client ko send karo                                                 |
| PUT    | Client say aney waley data server par majood named resource mey store karo, used while updating a resrouce on server |
| POST   | Client say aney waley data ko server per store karo                                                                  |
| DELTE  | Delete the named resource from the server                                                                            |
| HEAD   | Send just the HTTP headers from the response for the named resource.                                                 |

> **NOTE:** A server may implement their own request methods in addition to these. These additional methods are called extension methods.

## Status Code

Every HTTP response message comes back with a status code. The status code is a three-digit numeric code that tells the client if the request succeeded, or if other actions are required. Some of the HTTP status codes:-

#### Reson Phrase

Server aik reson pharse bhi send karta hey status code k sath jesay OK, Not Found etc.

| HTTP Status Code | Description                                      |
| ---------------- | ------------------------------------------------ |
| 200              | OK. Document returned correctly                  |
| 302              | Redirect. Go someplace else to get the resource. |
| 404              | Not Found. Can’t find this resource.             |

## Types of HTTP Message

There is only two type of HTTP messages:-

**Request Message**

An HTTP request sent from client side to server is called HTTP request message.

**Response Message**

A response sent from server to back to the client is called HTTP response message.

## Part of n HTTP Message

![Screenshot 2025-10-16 094506.png](C:\Users\mrasi\OneDrive\Node%20JS\Notes%20Pictures\Screenshot%202025-10-16%20094506.png)

HTTP message consist of three parts:-

### 1. Start Line

Start line woh pehli line jo batati hey k request k sath kia karna hey for example:-

```bash
GET "/index.html" HTTP/1.0
```

Ya response kelye kia huwa, dosray lafzo request k baad response ka status kia hey

```http
HTTP/1.0 200 OK
```

### 2. Headers

Headers are meta data about request/response for example:-

```http
Content-type: application/json
Content-length: 234
```

>  Header aik blank line pay end hota hey

### 3. Body

Offen called as response body yeah aik container hey jo muktalif kisam ka data (text, images, audio etc.) carry karti hey woh data client say server ya phir vice versa.

# 
