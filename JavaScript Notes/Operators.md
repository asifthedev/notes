## Arithmetic Operators

```js
console.log(2**2); // 4;
```

## Comparison Operators

**Strict Equality**

Checks if two values are equal and of the same type, without performing type coercion.

```js
2 === "2" // false
```

**Strict Inequality**

Checks if two values are not equal or not of the same type.

```js
2 !== "3" // true
```

## Comparison with Null

Comparisons (`>`, `<`, `>=`, `<=`) convert `null` to a number (`0`).

Equality (`==`) does **not** convert `null` to `0`. Instead, `null` is only loosely equal to `undefined`.

```js
console.log(null >= 0); // true
console.log(null == 0); // fasle
console.log(null <= 0); // true
console.log(null > -1); // true
console.log(null < 0); // false
```

## Logical Operators

AND (&&)

OR (||)

NOT (!)

## Nullish Coalescing {Ko-Aaa-Lacing} Operator

Returns its right-hand side operand when its left-hand side operand is `null` or `undefined`

Returns its left-hand side operand otherwise (even if it's `0`, `false`, or an empty string `""`.

```js
console.log(null ?? 'default') // default
console.log(0 ?? 'default') // 0
```


