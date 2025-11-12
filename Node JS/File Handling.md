# File Handling

The `fs` is a built in module used for file handling in Node JS. It stands for Files System.

fs mey files ko handle karney kelye synchronous (blocking code) and asynchronous dono type k functions available heyn. 

## How to read a file?

```js
const fs = require("node:fs")
fs.readFileSync('filePath', 'character-scheme')
```

Example:-

```js
const content = fs.readFileSync("./note.txt", "utf-8");
console.log(content);
```

## How write a file?

```js
const fs = require("node:fs");
const user = { name: "Asif", age: 22 };
fs.writeFileSync("user.json", JSON.stringify(user), "utf-8");
```

**Note:** `writeFileSync()` file ko overwrite kar deyta hey. Ager app overwrite k bajaye append karna chahtey ho file mey to:-

```js
const fs = require("node:fs");
fs.appendFileSync("note.txt", "\nI love JavaScript", "utf8");
```

## How to delte a file?

```js
fs.unlinkSync('filename')
```

## How to create a new directory?

```js
fs.mkdirSync("demo");
```

## How to remove a directory?

```js
fs.rmdirSync("./demo");
```

## Read and Write Asynchronously

Peaxhy ham ney abh jitnay function dehkay heyn woh sab syncronous ya blocking code hey, abh ham dehkay gey kis traha app aik file asyncronously read or wite kar saktey ho.

```js
const fs = require("node:fs");
fs.readFile("note.txt", "utf8", (err, data) => {
  if (err) {
    console.error("Error reading file:", err);
  } else {
    console.log("File contents:\n", data);
  }
});
```
