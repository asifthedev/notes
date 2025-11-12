# Middleware in Express.js

Middleware acts as an interceptor that sits between incoming requests and responses. It allows you to perform operations such as validation, authentication, and logging before the request reaches the actual endpoint.

**Syntax**

```js
app.use((req, res, next) => {
  console.log("LOGGER");
  next();
});
```

## Key Responsibilities of Middleware

1. Execute any code
2. Modify request/response objects
3. End the request-response cycle
4. Call the next middleware in the stack

## Types of Middleware

1. Application Level
2. Router Level
3. Error Handling
4. Built-in Middleware
5. Third-Party Middleware

## Application Level Middleware

Application-level middleware is attached to the main app instance using `app.use()` or bound to specific routes using `app.METHOD()`.

When you use `app.use()`, the middleware executes on **every request**, regardless of the endpoint.

**Example:** In this code snippet, the logger function runs on every request to any endpoint

```js
app.use((req, res, next) => {
  console.log("Logger");
  next();
});

app.get('/', (req, res) => res.send("Home"));
app.get('/users', (req, res) => res.send({name: "Asif"}));
```

You can also attach middleware to a **specific route**. In this example, the `logger` function is applied only to the home route `/`, so it runs only when requests are made to that route:

```js
function logger(req, res, next) {
  console.log("logger");
  next();
}

app.get("/", logger, (req, res) => {
  res.status(200).send("Hello, World!");
});
```

## Router Level Middleware

If you want to keep your code organized and execute middleware only on specific groups of endpoints, you can use a router instance:

```js
const adminRouter = express.Router();
```

For example, if you want to apply middleware only to admin-related endpoints, you can attach them to the router. These middlewares will execute only when requests are made to admin routes:

```js
const adminRouter = express.Router();

// This middleware only applies to admin routes
adminRouter.use(isAuthenticated);
adminRouter.use(isAdmin);
adminRouter.use(logAdminActivity);
```

In this setup, all middleware (authentication, authorization, logging) applies only to routes under `/admin/*`, keeping your code modular and maintainable.
