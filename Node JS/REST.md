# REST

It stands for **Representational State Transfor**, it's an Architectural Style for Network Based Applications. It's a set of rules that standardized the way of communication between client and server.

Ye ek **architectural style** hai (design pattern jaisa), jo define karta hai ke **client aur server kaise communicate karenge** network par.

**Set of Constraints/Rules** - REST wo rules hain jo tumhe follow karne hote hain taake tumhara API **scalable, maintainable, aur efficient** ho.

> **Not a Protocol** - REST khud koi protocol nahi hai (like HTTP), balke ye **guidelines** hain ke HTTP (ya koi aur protocol) ko **kaise use karna hai**

## **What are REST constraints?**

1. Client - Server Architecture 

2. Stateless 

3. Cachcable

4. Unifrom Interface

5. Layerd System

6. Code On Demand

## **1. Client–Server Architecture**

### **Definition**

Separation of concerns: The **client** handles the user interface and experience, while the **server** manages data and logic.  

Client or server elehda honey chaye.

### **Code Example**

```js
// client.js
fetch("https://api.example.com/users")
  .then(res => res.json())
  .then(data => console.log(data));

// server.js
import express from "express";
const app = express();

app.get("/users", (req, res) => {
  res.json([{ name: "Asif" }, { name: "Ali" }]);
});

app.listen(3000);
```

### **If Violated**

- UI code and server logic get tightly coupled.

- Any small change in the backend can break the frontend.

- Scalability and reusability suffer (e.g., mobile app and web can’t reuse the same backend easily).

And what if you have multiple clients, like mobile app and website, and desktop in that case server and client sepration will help you to use once single server for multiple clients.

## **2. Statelessness**

### **Definition**

Each request from client to server **must contain all the information** the server needs to fulfill it.  
The server should **not store any session state** between requests.

### **Analogy**

Imagine every customer at a coffee shop must tell their **entire order each time** — not rely on the barista remembering yesterday’s order.

### **Code Example**

```js
// Good: Stateless API (sends all info per request)
// server.js
import express from "express";
const app = express();

let loggedInUser = null;

app.post("/login", (req, res) => {
  loggedInUser = { id: 101, name: "Asif" }; // stored in memory
  res.send("User logged in!");
});

app.get("/dashboard", (req, res) => {
  if (loggedInUser) res.send(`Welcome ${loggedInUser.name}`);
  else res.status(401).send("Please log in");
});

app.listen(3000);
```

### **If Violated**

- Servers become overloaded managing session data.

- Load balancing and caching become complex.

- Crashes or restarts cause session loss.

---

## **3. Cacheability**

### **Definition**

Responses must define themselves as **cacheable** or **non-cacheable**, so clients or intermediaries can reuse data when appropriate.

### **Analogy**

Imagine your phone’s map app caching downloaded tiles — it doesn’t fetch the same street map every second.

### **Code Example**

```js
// Cacheable response
app.get("/products", (req, res) => {
  res.set("Cache-Control", "public, max-age=3600"); // 1 hour
  res.json([{ id: 1, name: "Tea" }]);
});
```

### **If Violated**

- Increased latency and server load.

- Clients repeatedly fetch identical data.

- Poor scalability and performance.

---

## **4. Uniform Interface**

### **Definition**

A consistent, standardized interface between client and server.  
Usually achieved through **HTTP verbs (GET, POST, PUT, DELETE)** and **resource-based URIs**.

### **Analogy**

Think of USB ports — any USB device can connect because they share a standard interface.

### **Code Example**

```js
// Uniform REST API
app.get("/users", ...);       // Retrieve users
app.post("/users", ...);      // Create user
app.put("/users/:id", ...);   // Update user
app.delete("/users/:id", ...);// Delete user
```

### **If Violated**

- APIs become confusing and inconsistent.

- Client developers struggle to integrate.

## **5. Layered System**

### **Definition**

A REST system is composed of **hierarchical layers** — clients don’t need to know whether they’re talking directly to the server or an intermediary (like a cache, proxy, or load balancer).

### **Analogy**

Like a **postal system** — you drop a letter in a mailbox, unaware of how many centers it passes through.

### **Code Example**

```js
// Example architecture
// Client -> CDN -> Load Balancer -> App Server -> Database
```

In Node.js, middleware or reverse proxies like **Nginx** act as layers:

```js
app.use((req, res, next) => {
  console.log("Layer 1: Logging");
  next();
});

app.use("/api", (req, res) => {
  res.send("Final layer reached");
});
```

### **If Violated**

- Scalability and flexibility decline.

- Security layers (like firewalls or gateways) can’t be inserted easily.

- Systems become brittle and hard to maintain.

---

## **6. Code on Demand (Optional)**

### **Definition**

Servers can extend client functionality by **sending executable code**, like JavaScript, to be run on the client.

### **Analogy**

A website sending a **script** to enhance interactivity — similar to giving someone instructions to perform a task instead of doing it for them.

### **Code Example**

```js
// Server sends executable code
app.get("/script", (req, res) => {
  res.type("application/javascript");
  res.send(`alert("Dynamic code delivered from server!");`);
});
```

### **If Violated**

- No major issue (it’s optional), but less flexibility.

- Some applications might require server-side updates for things that could be handled dynamically on clients.

- However, **overuse can reduce security and visibility**.

## **Summary Table**

| Constraint        | Purpose                  | Example                     | Violation Consequence          |
| ----------------- | ------------------------ | --------------------------- | ------------------------------ |
| Client–Server     | Separation of UI & logic | Frontend–Backend split      | Tight coupling                 |
| Stateless         | Each request independent | Include all info in headers | Session dependency             |
| Cacheable         | Improve performance      | Cache-Control headers       | Slower response, more load     |
| Uniform Interface | Consistent interaction   | Use HTTP verbs              | Confusion, poor reuse          |
| Layered System    | Scalability via layers   | CDN, proxies, middleware    | Hard to scale                  |
| Code on Demand    | Extend client            | Send JS from server         | Optional, but risky if misused |

---


