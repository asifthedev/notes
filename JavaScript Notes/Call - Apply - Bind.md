In JavaScript, `call`, `apply`, and `bind` are methods used to control the execution context of functions, specifically the value of the `this` keyword inside the function. They are also used for function borrowing.

## Call

It invokes the function immediately with a specified value of `this`  and arguments provided individually.

```js
let obj = {
  name: "Asif",
};

function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

greet.call(obj, "Hello");
```

Let see an example of function borrowing using `call()`

```js
let obj = {
  name: "Asif",
  greet: function () {
    console.log(`Hello, ${this.name}`);
  },
};

let obj2 = {
  name: "Asim",
};

obj.greet.call(obj2); // Hello, Asim
```

**Argument Passing**
With `call()` method you can also pass arguments to the function. The first argument is must be the execution context or value for `this`, after it you can pass all of your arguments separated by comma `(,)`

```js
let obj = {
  name: "Asif",
  age: 21,
};

function whoami(name, age) {
  console.log(`My name is ${name} and I'm ${age} years old.`);
}

whoami.call(obj, "Asif", 21);
```

## Apply

Invokes a function immediately with a specified `this` value and arguments provided as *an array (or an array-like object)*. 

```js
let obj = {
  name: "Asif",
  age: 21,
};

function whoami(name, age) {
  console.log(`My name is ${name} and I'm ${age} years old.`);
}

whoami.apply(obj, ["Asif", 21]);
```

## Bind

`call()` and `apply()` invoke the function immediately, while `bind()` returns a new function that can be invoked later.

```js
let obj = {
  name: "Asif",
  age: 21,
  mail: "info@asifshahzad.me",
};

function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}

let bindingGreet = greet.bind(obj, greeting); 

bindingGreet();
```

Creates a new function that, when called, has its `this` keyword permanently bound to the provided value `obj`. It can also pre-set arguments. The new function is not invoked immediately.