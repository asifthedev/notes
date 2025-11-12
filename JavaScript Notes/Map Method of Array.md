- `map()` is a method used to **transform each element** in an array.
- It returns a **new array** with the **same length** as the original.
- The original array remains **unchanged**.
- It takes a **callback function** as input.
- The callback runs on **every element** and returns the **new value** for that position.

### Example:

```js
let nums = [1, 2, 3];
let output = nums.map((x) => x > 2); // [ false, false, true ]
console.log(output);
```

Create HTML List Items

```js
const items = ["Apple", "Banana"];
const html = items.map(item => `<li>${item}</li>`);
console.log(html); // ["<li>Apple</li>", "<li>Banana</li>"]
```
### Key Points:

- Use `map()` when you want to **create a new version** of the array.
- It’s useful for **data transformation** (like formatting, multiplying, or extracting)