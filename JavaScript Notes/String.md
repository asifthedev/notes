## String

In JavaScript, a string is a primitive data type used to represent textual data. It is a sequence of characters, which can include letters, numbers, symbols, words, or sentences.

**Immutability**

Once a string is created, its content cannot be directly changed. Any operation that appears to "modify" a string, such as converting it to uppercase or extracting a substring, actually results in the creation of a new string with the desired changes. The original string remains unchanged in memory.

**Indexing:**

Characters within a string are accessed by their index, starting from 0 for the first character.

## Methods

### toUpperCase()

```js
let str = 'Hello, JavaScript!'
console.log(str.toUpperCase()); // HELLO, JAVASCRIPT!
```

### toLowerCase()

```js
let str = 'Hello, JavaScript'
console.log(str.toLowerCase()) // hello, javascript!
```

### indexOf()

It is used to find the first occurrence of a specified value within a string or an array. It returns the index (position) of the first character or element found, or -1 if the value is not present.

**Syntax**

```js
str.indexOf(substring, fromIndex)
```

`searchValue`: The substring to search for.

`fromIndex` (optional): The index from which to start the search. If omitted, the search starts from the beginning (index 0).

```js
let text = "Hello World";
let index1 = text.indexOf("World"); // Returns 6
let index2 = text.indexOf("world"); // Returns -1 (case-sensitive)
let index3 = text.indexOf("o", 5); // Returns 7
```

### charAt()

It is used to retrieve a character at a specified index within a string.

**Syntax**

```js
str.chartAt(index)
```

**Parameters**

`index`: An integer representing the position of the character to be retrieved. The index is zero-based, meaning the first character is at index 0, the second at index 1, and so on. If no index is provided, it defaults to 0.

**Return Value**

The character at the specified `index` within the string.

An empty string (`""`) if the `index` is out of bounds (e.g., negative or greater than or equal to the string's length).

```js
const myString = "Hello World";

console.log(myString.charAt(0)); // Output: H
console.log(myString.charAt(4)); // Output: o
console.log(myString.charAt(100)); // Output: "" index out of bounds
```

### lastIndexOf()

`lastIndexOf()` method is used to find the last occurrence of a specified value within a string or an array. This method searches a string from the end towards the beginning and returns the index of the last occurrence of a specified substring.

**Syntax**

```js
str.lastIndexOf(value, fromIndex)
```

`value` string value you want to search for their last index

`fromIndex`, which specifies the index from which to start the search (searching backwards from this index).

```js
let str = 'hello, world hello'
console.log(str.lastIndexOf('hello', 7)); // 4
```

### substring()

The `substring()` method is used to extract a portion of a string and return it as a new string. This method does not modify the original string.

**Syntax**

```js
str.substring(startIndex, endIndex)
```

Parameters:

- `startIndex`: The index of the first character to include in the returned substring. This index is zero-based.
- `endIndex` (optional): The index of the first character to exclude from the returned substring. If omitted, the substring will extend to the end of the original string. 

Behavior:

- The `substring()` method extracts characters from `startIndex` up to, but not including, `endIndex`.
- If `startIndex` is greater than `endIndex`, the `substring()` method will swap the two arguments internally, effectively treating the smaller value as `startIndex` and the larger value as `endIndex`.
- If either `startIndex` or `endIndex` is negative or `NaN`, they are treated as `0`

```js
const originalString = "Hello, World!";

// Extract from index 0 up to (but not including) index 5
const sub1 = originalString.substring(0, 5); // "Hello"

// Extract from index 7 to the end of the string
const sub2 = originalString.substring(7); // "World!"

// Example with swapped indices (startIndex > endIndex)
 // "Hello" (treated as substring(0, 5))
const sub3 = originalString.substring(5, 0);

// Example with negative index (treated as 0)
// "Hello" (treated as substring(0, 5))
const sub4 = originalString.substring(-5, 5); 
```

## slice()

 The `slice()` method is used to extract a portion of an array or a string and return it as a new array or string, respectively. It does not modify the original array or string.

**Syntax:**

```js
str.slice(startIndex, endIndex)
```

- **Parameters:**
  - `startIndex` (optional): The index at which to begin extraction. If omitted, it defaults to 0.
  - `endIndex` (optional): The index before which to end extraction. The character at `endIndex` is not included. If omitted, `slice()` extracts to the end of the string.
- **Return Value:** A new string containing the extracted characters.

### trim()

It's used to remove preceding and trailing spaces in string.

```js
let str = " Asif " // Asif
```

There are also a method `trimLeft()` and `trimRight()`

### replace()

The `replace()` method in JavaScript is a string method used to replace a substring within a string with another substring. It returns a new string with the replacement, leaving the original string unchanged. 

**Syntax:**

```js
string.replace(searchValue, newValue)
```

**Parameters:**

- `searchValue`:
  
  This can be either:
  
  - A string to be searched for. In this case, only the first occurrence of the `searchValue` will be replaced.
  - A regular expression (RegEx). This allows for more powerful pattern matching and can be used with flags (like `g` for global replacement, `i` for case-insensitive replacement) to control the replacement behavior.

- `newValue`:
  
  This can be either:
  
  - A string to replace the `searchValue`.
  - A function that will be called for each match, and its return value will be used as the replacement string.
  
  ### replaceAll()
  
   Same as replace() but it will replace all of the matching occurrences not just first one.
  
  ```js
  let str = "Asif is a good man. Asif love coding"
  console.log(str.replaceAll("Asif", "Asim"))
  // "Asim is a good man. Asim love coding"
  ```

### includes()

The `includes()` method in JavaScript is a built-in function used to determine whether a string or an array contains a specified value. It returns `true` if the value is found and `false` otherwise. This method is case-sensiti

```js
let str = "Congratulations"
console.log(str.includes("Congrat")) // true
```

### split()

It split or divide the string into an ordered list of substrings and converts it into an array by following the pattern for given seprator.

**Syntax**

```js
string.split(separator, limit);
```

**Parameters:**

- `separator` (Optional):
  
  This specifies the character, sequence of characters, or regular expression that defines where the string should be split.
  
  - If `separator` is omitted, the entire string is returned as a single element in the array.
  - If `separator` is an empty string (`""`), the string is split into an array of individual characters.

- `limit` (Optional):
  
  This is an integer that specifies the maximum number of splits to be found. If the `limit` is reached, any remaining parts of the string are not included in the resulting array.

```js
let str = "banana,mango,apple"
console.log(str.split(",", 2)) // [banana, mango]
```

### repeat()

```js
let mood = "Happy! "
console.log(`I feel ${mood.repeat(3)}`); //I feel Happy! Happy! Happy!
```

### startWith()

```js
let str = "I love code"
console.log(str.startsWith("I")); //true
```

### endsWith()

```js
let str = "I love code"
console.log(str.endsWith("code")); // true
```
