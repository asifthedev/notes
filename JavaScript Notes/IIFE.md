An IIFE, or Immediately Invoked Function Expression, is a JavaScript function that executes as soon as it is defined. It is also known as a self-executing anonymous function.

**A Function Expression:** This is usually an anonymous function (a function without a name), which is enclosed in parentheses to make it a function expression rather than a function declaration.

```js
(function() {
    // Function body
});
```

 **Immediate Invocation:** Immediately following the closing parenthesis of the function expression, another set of parentheses `()` is added to invoke the function.

```js
(function() {
    // Function body
})();
```

****