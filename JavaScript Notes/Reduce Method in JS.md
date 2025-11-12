The `reduce()` method executes a **reducer function** on each element of an array, **resulting in a single output value**.
## Syntax:

```js
array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue)
```

### Parameters:

| Parameter      | Description                                                     |
| -------------- | --------------------------------------------------------------- |
| `callback`     | Function that executes on each element                          |
| `accumulator`  | Accumulates the result across iterations (like a rolling total) |
| `currentValue` | The current element being processed                             |
| `currentIndex` | (Optional) Index of the current element                         |
| `array`        | (Optional) The array `reduce()` was called on                   |
| `initialValue` | (Optional) Value to use as the first `accumulator`              |

---

## Simple Example:

```javascript
const numbers = [1, 2, 3, 4, 5];

const sum = numbers.reduce((acc, curr) => acc + curr, 0);

console.log(sum); // Output: 15
```

---

## 🔹 Without `initialValue`:

```javascript
const numbers = [10, 20, 30];

const result = numbers.reduce((acc, curr) => acc + curr);

console.log(result); // Output: 60
```

⚠️ If `initialValue` is not provided:
- `accumulator` is set to the first element
- `currentValue` starts from second element

## 🔹 `reduceRight()`: The reverse cousin

Just like `reduce()`, but processes array **right to left**.

```javascript
['a', 'b', 'c'].reduceRight((acc, curr) => acc + curr); // Output: 'cba'
```

## Summary

|Feature|Explanation|
|---|---|
|Purpose|Reduce array to a single value|
|Input|Callback and optional initial value|
|Output|One accumulated value|
|Pure Function|Yes, should be pure|
|Use with|Sum, average, max, count, flatten, etc.|
