The `for...of` loop in JavaScript provides a concise way to iterate over the values of iterable objects.

Built-in Iterable Objects in JavaScript:
- **Arrays:** `[1, 2, 3]`
- **Strings:** `"hello"`
- **Maps:** `new Map([['a', 1], ['b', 2]])`
- **Sets:** `new Set([1, 2, 3])`
- **TypedArrays:** `new Int8Array([1, 2, 3])`

It simplifies looping compared to traditional `for` loops when dealing with data structures that have an iterable protocol. Syntax:

```js
for (const element of object) {

}
```

**For of loop over Array**
```js
let arr = [1, 2, 3];

for (const number of arr) {
  console.log(number); 
}

// 1 2 3
```

**For of loop over Map**
```js
let map = new Map([
  ["ST01", { name: "Asif", age: 21 }],
  ["ST02", { name: "Asim", age: 25 }],
]);

for (const student of map) {
  console.log(student);
  // Output
  // ["ST01", { name: "Asif", age: 21 }]
  // [("ST02", { name: "Asim", age: 25 })];
};
```

But some time you want the key and value in separate variables like in this case you want the student id and it's value to hold in different variables:

```js
for (const [id, student] of map) {
  console.log(student);
}
```

**For of over String**

```js
let name = "Asif";
for (const letter of name) {
  console.log(letter);
}
// A s i f
```