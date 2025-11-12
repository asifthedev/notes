In JavaScript, the `Map` object is a collection of key-value pairs where keys can be of any data type (including objects or primitive values), and it remembers the original insertion order of the keys. This distinguishes it from plain JavaScript objects, where keys are typically limited to strings and symbols, and property order is not guaranteed.

- **Key-Value Pairs:** Stores data as unique key-value pairs.
- **Arbitrary Key Types:** Keys can be any data type, including objects, functions, or primitive values like numbers and booleans.
- **Insertion Order Preservation:** The order in which elements are inserted into the Map is preserved during iteration.
- **Iterability:** Maps are iterable, allowing for easy traversal of their key-value pairs using constructs like `for...of` loops.

**How to create map object?**
A `Map` object can be created using the `new Map()` constructor:
```js
let map = new Map()
```

Or, by passing an array of key-value pair arrays:
```js
let map = new Map([
["CPP", "C++"],
["JS", "JavaScript"]
])
```

**Common Map Methods and Properties**:

 `set(key, value)`: Adds or updates a key-value pair.
```js
map.set("py", "Python") 
// Map(3) { 'CPP' => 'C++', 'JS' => 'JavaScript', 'py' => 'Python' }
```
 
`get(key)`: Retrieves the value associated with a given key.
```js
map.get("CPP") // C++
```

`has(key)`: Checks if a key exists in the Map.
```js
console.log(map.has("CPP")); // true
```

 `delete(key)`: Removes a key-value pair by its key.
```js
map.delete("CPP");
console.log(map); // Map(2) { 'JS' => 'JavaScript', 'py' => 'Python' }
```

 `size`: Returns the number of key-value pairs in the Map.
```js
console.log(map.size) // 2
```

`clear()`: Removes all key-value pairs from the Map.

```js
map.clear()
```

