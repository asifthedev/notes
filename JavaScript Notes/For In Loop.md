It's used to iterate over the enumerable keys of the an object. Enumerable keys are those on which we can loop through using `for...in` or those which we can list out using `Object.keys()` method.

`for...in` loop is primarily designed for iterating over object properties.

```js
let user = { name: "Asif", age: 21 };

for (const key in user) {
  console.log(`${key} is: ${user[key]}`);
}
// name is: Asif
// age is: 21
```
