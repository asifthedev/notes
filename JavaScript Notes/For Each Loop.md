
### What is `forEach`?

`forEach` is a **built-in method of an Array in JavaScript** that allows you to **loop through each element in an array** and perform some action on every item.

Instead of writing a traditional `for` loop, `forEach` gives you a cleaner and more readable way to handle arrays.

### How does it work?

The `forEach` method takes a **callback function** as an argument. This callback function is **automatically called once for every element in the array**.

The callback function implicitly receives **up to three arguments** those all are:

1. **Current Value** – The value of the current element being processed
2. **Current Index** – The index (position) of the current element
3. **The Full Array** – The original array you are looping through

### Syntax:

```js
array.forEach(function(currentValue, index, array) {
  // Your code here
});
```

Or with arrow function:

```js
array.forEach((currentValue, index, array) => {
  // Your code here
});
```

---

### Example:

```js
const fruits = ['apple', 'banana', 'cherry'];

fruits.forEach(function(fruit, index, fullArray) {
  console.log(`Fruit at index ${index} is ${fruit}`);
});
```

**Output:**

```
Fruit at index 0 is apple  
Fruit at index 1 is banana  
Fruit at index 2 is cherry
```

### Notes:

- `forEach` does **not return anything** (it returns `undefined`)
- It is used mainly for **performing side effects** like printing, updating the UI, etc.
- You **cannot break or exit early** from a `forEach` loop (unlike `for`, `for...of`, or `for...in`)

### Compared to `map()`:

- `forEach` is for **looping with side effects**
- `map` is for **transforming arrays** and returns a **new array**