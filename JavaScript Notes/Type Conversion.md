## Type Conversion

To convert a primitive data type to another primitive data type, you can do:

```js
let age = "22"
let num = Number(age)
```

Let see some examples of how various type of values in particular data type behave when converting them to another data type.

```js
let num = "123abc"
let num2 = Number(num) // NaN -> Type number


let emptyString = "";
console.log(Boolean(emptyString)) // false

let name = "Asif";
console.log(Boolean(name)) // true

// Number -> Boolean
// 1 -> true
// 0 -> false
```

## Falsy & Truthy

In JavaScript, values that are not explicitly `true` or `false` can still be evaluated as "truthy" or "falsy" in a boolean context. The "falsy" values are:

- `false`
- `0` (the number zero)
- `""` (an empty string)
- `null`
- `undefined`
- `NaN` (Not a Number)

All other values are considered "truthy."

```js
console.log(Boolean(0)); // false
console.log(Boolean("")); // false
console.log(Boolean(null)); // false
console.log(Boolean(undefined)); // false
console.log(Boolean(NaN)); // false
```

## Conversion of Null

Comparisons (`>`, `<`, `>=`, `<=`) convert `null` to a number (`0`).

Equality (`==`) does **not** convert `null` to `0`. Instead, `null` is only loosely equal to `undefined`.

```js
console.log(null >= 0); // true
console.log(null == 0); // false
console.log(null <= 0); // true
console.log(null > -1); // true
console.log(null < 0); // false
```
