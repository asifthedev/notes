# Math

Mathematical operations and functions are primarily handled through the built-in `Math` object. This object is a global object and does not require instantiation using a constructor. All its properties and methods are static, meaning they are accessed directly using `Math.` followed by the property or method name.

## Methods

### toFixed()

It's is built-in method for the number prototype used to format a number by converting it into a string and rounding it to a specified decimal places.

**Syntax**

```js
number.toFixed(digits)
```

**Parameters:**

- `digits` (Optional): An integer specifying the number of digits to appear after the decimal point. If omitted, it defaults to 0, rounding the number to the nearest whole number. This value must be between 0 and 100, inclusive; otherwise, a `RangeError` is thrown.

**Return Value:**

The `toFixed()` method returns a string representing the given number formatted with the specified number of decimal places.

**Padding with Zeros:**

If the specified `digits` value is greater than the actual number of decimal places in the original number, the fractional part of the string is padded with trailing zeros to reach the desired length.

```js
let num1 = 123.45678;
console.log(num1.toFixed(2)); // Outputs: "123.46" (rounded)

let num2 = 10.5;
console.log(num2.toFixed(4)); // Outputs: "10.5000" (padded with zeros)

let num3 = 5.23;
console.log(num3.toFixed(0)); // Outputs: "5"

let num4 = 9.999;
console.log(num4.toFixed(2)); // Outputs: "10.00" 
```

### toLocalString()

It's used for dates and numbers. For numbers, it's used to format the number according to the given language and specified format.

```js
let num4 = 1560320;
console.log(num4.toLocaleString("en-IN")); // 15,60,320
```

## round()

The `Math.round()` function is a static method of the built-in `Math` object that returns the value of a number rounded to the nearest integer.

**How it works:**

- It rounds a number up if the decimal part is `0.5` or greater.
- It rounds a number down if the decimal part is less than `0.5`.

**Syntax:**

```javascript
Math.round(x);
```

- `x`: The number you want to round.

```js
let num = 4.32;
console.log(Math.round(num)); // 4

let num2 = 4.56;
console.log(Math.round(num2)); // 5
```

### floor()

The `Math.floor()` function in JavaScript rounds a number down to the nearest whole integer. This means it returns the largest integer less than or equal to the given number.

**Positive Number**

```js
Math.floor(3.99); // Returns 3
Math.floor(5.19); // Returns 5
```

**Negative Number**

```js
// (because -90 is the largest integer less than or equal to -89.02)
Math.floor(-89.02); // Returns -90 
Math.floor(-4.9);   // Returns -5
```

## ceil()

In JavaScript, `ceil` refers to the `Math.ceil()` method, which is used to round a number upwards to the nearest whole integer.

```js

```

### max()

```js
console.log(Math.max(1, 2, 3)) // 3
```

### min()

```js
console.log(Math.min(1, 2, 3)) // 1
```

## random()

One of the most used methods offered by the Math object. It always ret
