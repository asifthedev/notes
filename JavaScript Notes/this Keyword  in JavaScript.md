## Global Space

**Node JS**
In node in global space this refers to the `module.exports` object and it's empty by default. If `this` and `module.exports` are same object then assigning value to one of them will reflects in both  as they are the same objects.

**Test Case in Node**
```js
this.name = "Asif";
module.exports.age = 32;
console.log(module.exports) // {name: "Asif", age: 32}
```

**Browser**
In browser  `this` refers to global object which is window object. If you type this in browser's console you will have windows object as an output.
```js
> this
> Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}
```

## Function Level

The value of the `this` inside regular function is undefined in strict mode. But in non strict mode due to the this substitution mechanism of JavaScript (whenever the value of this is equal to undefined or null it will be replaced with global object) `this keyword` refers to the global/window object.

**Non Strict Mode**
In regular function in non *strict mode* this refers to **global object** in node and **window** object in browser.

```js
function fx() {
  console.log(this); // Node: global object, Browser: window object
}
```

**Strict Mode**
The keyword this inside a regular function is `undefined` in both in the browser and inside node.

```js
"use strict"
function fx() {
  console.log(this); // Node: undefined, Browser: undefined
}
```

## this And Object

In general it said that `this` refers to the current object calling the function. 
```js
function fx() {
  console.log(this);
}   
window.fx(); // this -> window object
```

If a function is defined inside an object as a method then `this` refers to current object calling the function.
```js
let user = {
  name: "Asif",
  greet: function fx() {
    console.log(this);
  },
};

user.greet(); // { name: 'Asif', greet: [Function: fx] }
```

## this with Call, Apply, Bind Methods

In **JavaScript**, when you use **`call`**, **`apply`**, or **`bind`**, the `this` keyword **refers to the context (object) you explicitly provide** as the first argument.

```js
function sayHello() {
  console.log(this);
} 

const user = { name: "Asif" };
sayHello.call(user); // { name: "Asif" }
```

## this Inside Arrow Function

Arrow functions don't have their own `this` binding or they don't provide this instead they inherit this from their lexical scope. 

**What is Lexical Scop?**
[Lexical scop](https://www.freecodecamp.org/news/javascript-lexical-scope-tutorial/) mean the place where a variable actually defined, it doesn't matter where the variable or functions is used or invoked. The lexical scope refers to place of definition for an item in JavaScript.

```js
let name = "Asif"
```
The lexical scop is global because the variable is defined in the global space.

```js
function greet(){
  let name = "Asim"
}
```

Now the lexical scop for variable name is `greet()` because it's defined inside it.

### Object Littrell is Not a Scop
It’s possible that you might get confused by the curly brackets in an object literal and think they create a scope — but let me tell you, they do not. An object is just a container for properties, not a scope.

```js
let obj = {name: "Asif"}
```

### JavaScript creates a new **scope** only in these three places:

1. **Block Scope** – created with `{}` when used with `let`, `const`, or `class`
2. **Function Scope** – inside function bodies    
3. **Module Scope** – in ES6 modules (each module has its own top-level scope)

Now we've learned everything required to understand `this` inside arrow function let's see the first code example:
```js
let obj = {
  name: "Asif",
  greet: () => {
    console.log(this);
  },
};

console.log(obj.greet())
```

What you think the `this` keyword is referring to? It inherits this value from it's lexical scop or context, which is in this case is global space in this case which is global as we've already learned the object is not a scop.

## `this` Inside Nested Arrow Function

```js
let obj = {
  name: "Asif",
  greet: function fx() {
    let x = () => {
      console.log(this);
    };
    x();
  },
};

obj.greet();
```

As we know the value of this in arrow function is comes from it's lexical context or scop and lexical scop or context mean where the function is defined. So in given code the value of this in arrow function comes from it's lexical scop which is the `fx()` function and `fx()` is the method of `obj` where this is pointing to  `obj` object. So the value of this inside arrow function is the object `obj`

## this Inside DOM Elements

`this` points to the HTML Element in DOM

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Test Page</title>
  </head>
  <body>
    <button onclick="alert(this)">Click Me</button>
    <script src="test.js"></script>
  </body>
</html>
```

Output as I clicked on button: 

![[Pasted image 20250705182036.png]]