## Problem

HTTP is a stateless protocol, hay, yani har request serve karnay k baad server yeah bhool jata hey k pichli bar kia huwa tha. 

Yani ager mey aik page per login karta hun to aglay page per server meyri login state bhool jaya ga. Yeah maslay ko hal karnay kelye server aik specific time period kelye app ki state ko yaad rakhta hey.

Yeah, problem ko session or cookies ki help say solve kia jata hey.

## What is a Session?

A session is the period of time during which a user interacts with a website/application, from login to logout (or timeout).

## What is a Session ID?

Jab user successfully login ya register ho jata hey to uskelye aik session ID (mostly an alpha-numeric string) generate kar di jati hey takey usay bar bar khud authenticate karwanay kelye password or email na dalni parey.

Agli request per woh server ko ja k wahi id dhikata hey server id ko validate karta hey or ager id server k pass majod id say match ho jati hey to usay access dey di jati hey.

## What are Cookies?

In web server terms, **cookies** are small pieces of data that a web server sends to a user's browser, which the browser then stores and sends back to the server with subsequent requests.

**Server sends cookie**: When you visit a website, the server can send a cookie to your browser via an HTTP response header

**Browser stores it**: Your browser saves this cookie locally

**Browser returns it**: On future requests to that same server, your browser automatically includes the cookie in the HTTP request headers

**Server reads it**: The server can then read the cookie data to recognize you or recall information about your session

### Note on Cookies

Chrome allows 180 cookies per domain with a size limit of 4KB for each cookie, and the time period you can store those cookies is 400 days.

Cookies are stored as pairs:

- **Name** = The identifier/key (e.g., "username")
- **Value** = The actual data (e.g., "john_doe")

## Local Storage

**Local storage** in a browser is a mechanism that allows web applications to **store data persistently** within the user's browser, with **no expiration date**. 

This means the data remains available even after the user closes the browser window, the tab, or restarts their computer

LocalStorage typically allows about 5 MB of storage per domain/website

## **IndexedDB**

A more advanced browser database system that:

Can store much larger amounts of data (often 50MB+ or even unlimited with user permission)

Supports complex data structures (not just strings like LocalStorage)

Works like a real database with indexes, queries, and transactions

- Good for offline web applications
