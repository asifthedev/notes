# Most Asked JavaScript Interview Concepts

## 1. **Variables & Scope**

- `var`, `let`, `const` difference

- Function scope vs Block scope

- Temporal Dead Zone (TDZ)

```js
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 10;
```

---

## 2. **Hoisting**

- JS execution me declarations upar uth jati hain.

- Functions complete hoist hoti hain, variables sirf declaration.

```js
sayHi(); // works
function sayHi() { console.log("Hi"); }
```

---

## 3. **Closures**

- Function jo apne outer scope ke variables ko yaad rakhta hai.

```js
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  }
}
let counter = outer();
console.log(counter()); // 1
console.log(counter()); // 2
```

---

## 4. **this Keyword**

- Value context pe depend karti hai:
  
  - Object method → object
  
  - Normal function → `undefined` (strict mode) / global (non-strict)
  
  - Arrow function → lexical `this`

---

## 5. **Promises & Async/Await**

- Asynchronous programming ke liye.

```js
async function fetchData() {
  let res = await fetch("https://api.example.com");
  let data = await res.json();
  console.log(data);
}
```

---

## 6. **Event Loop & Concurrency**

- Call stack, Web APIs, Callback Queue, Microtasks.

- `setTimeout`, `Promise`, `async/await` ka behavior.

---

## 7. **Prototype & Inheritance**

- JS objects prototype chain use karte hain.

```js
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function() {
  console.log("Hi " + this.name);
};
```

---

## 8. **Higher-Order Functions**

- Functions jo dusre functions ko accept return karte hain. (`map`, `filter`, `reduce`)

```js
let nums = [1,2,3];
let squared = nums.map(n => n*n);
```

---

## 9. **Type Coercion**

- JS weakly typed hai → automatic type conversion.

```js
console.log("5" - 2); // 3
console.log("5" + 2); // "52"
```

---

## 10. **Equality (== vs ===)**

- `==` → loose comparison (type coercion)

- `===` → strict comparison

---

## 11. **Event Bubbling & Capturing**

- Events DOM me propagate karte hain.

```js
element.addEventListener("click", handler, true); // capture
```

---

## 12. **Modules (import/export)**

- Modern JS me code organize karne ka tareeqa.

```js
// math.js
export function add(a,b){ return a+b; }

// main.js
import { add } from './math.js';
```

---

## 13. **Error Handling**

- `try...catch...finally`

- Custom errors

---

## 14. **ES6+ Features**

- Destructuring

- Spread & Rest operator

- Template literals

- Default params

---

## 15. **Common Built-in Objects**

- `Date`, `Math`, `JSON`

- `Object.keys()`, `Object.values()`, `Object.entries()`

---

⚡ Bonus (advanced interview topics):

- Debouncing & Throttlinga

- Currying

- Shallow vs Deep copy (`Object.assign`, `structuredClone`)

- `call`, `apply`, `bind`

- Garbage collection basics
