
- `filter()` is a method used to **iterate over an array**.
- It performs a **conditional check** on each element.
- It returns a **new array** with only the elements that **meet the condition**.
- The **original array remains unchanged**.
- It takes a **callback function** that returns `true` (keep the item) or `false` (discard it).

### Example

```js
const numbers = [1, 2, 3, 4, 5];
const even = numbers.filter(num => num % 2 === 0);
console.log(even); // [2, 4]
```