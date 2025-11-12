## How to formated JSON response?

Everytime I develop an API I'll send prettier JSON!

```js
app.set('json spaces', 2)
```

## JSON Standard to Follow

Collection+JSON is a **JSON-based media type** designed specifically for managing and querying collections of data through RESTful APIs. It was created by Mike Amundsen as a hypermedia format that provides a standardized way to represent collections.

## What It Looks Like

Here's a basic example of a Collection+JSON document:

```json
{
  "collection": {
    "version": "1.0",
    "href": "https://api.example.com/users",

    "links": [
      {"rel": "feed", "href": "https://api.example.com/users/feed"}
    ],

    "items": [
      {
        "href": "https://api.example.com/users/123",
        "data": [
          {"name": "name", "value": "John Doe"},
          {"name": "email", "value": "john@example.com"},
          {"name": "age", "value": 30}
        ],
        "links": [
          {"rel": "profile", "href": "https://api.example.com/users/123/profile"}
        ]
      },
      {
        "href": "https://api.example.com/users/456",
        "data": [
          {"name": "name", "value": "Jane Smith"},
          {"name": "email", "value": "jane@example.com"},
          {"name": "age", "value": 28}
        ]
      }
    ],

    "queries": [
      {
        "rel": "search",
        "href": "https://api.example.com/users/search",
        "data": [
          {"name": "name", "value": ""}
        ]
      }
    ],

    "template": {
      "data": [
        {"name": "name", "value": ""},
        {"name": "email", "value": ""},
        {"name": "age", "value": ""}
      ]
    }
  }
}
```

## Key Components

1. **collection** - The root object containing all data
2. **items** - Array of resources in the collection
3. **links** - Hypermedia links for navigation
4. **queries** - Predefined search/filter operations
5. **template** - Schema for creating new items
6. **error** - Error information (when applicable)

## Why It's Important for API Design

### 1. **Self-Descriptive APIs**

Collection+JSON makes APIs self-documenting. Clients can discover available operations without external documentation by examining the `template` and `queries` sections.

### 2. **HATEOAS Compliance**

It implements Hypermedia as the Engine of Application State (HATEOAS), a key constraint of REST. Clients navigate the API through hypermedia links rather than constructing URLs manually.

### 3. **Standardization**

Provides a consistent structure across different APIs, reducing the learning curve for developers and enabling generic client libraries.

### 4. **Write Operations Made Clear**

The `template` section explicitly shows what data is needed to create new resources, eliminating guesswork.

### 5. **Query Support**

The `queries` section advertises available search and filter operations, making APIs more discoverable.

### 6. **Decoupling**

Clients depend on link relations (`rel` attributes) rather than hardcoded URLs, allowing server-side URL changes without breaking clients.

### 7. **Uniform Interface**

Enforces a uniform structure that works across different domains, making it easier to build reusable tools and clients.

## Trade-offs

While powerful, Collection+JSON does add verbosity compared to simpler JSON formats. It's most valuable for:

- Public APIs with diverse clients
- Long-lived APIs where evolvability matters
- Systems requiring high discoverability

For simple internal APIs or when performance/payload size is critical, lighter-weight formats might be more appropriate.


