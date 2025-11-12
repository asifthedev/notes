# Regular Expression

Regular Expression, also known as Regex, is a sequence of characters that defines a search pattern.  It allows you to match, search, and replace text based on specific patterns.

In JavaScript, a regex pattern is enclosed within forward slashes (`/`), which tells the engine to treat it as a regular expression.

```js
const pattern = /cat/;
```

**test()**

You can use the `test()` method to check whether a string matches the pattern:

```js
const pattern = /cat/;
console.log(pattern.test("I love cats.")); // true
```

### Flags

A flag is a modifier that changes how the regex pattern behaves. The most commonly used flag is `g` (global), which tells the regex engine to find all occurrences of the pattern instead of stopping after the first match.

```js
const text = "cat cat cat"
const pattern = /cat/g;
console.log(text.match(pattern)); // ["cat", "cat", "cat"]
```


