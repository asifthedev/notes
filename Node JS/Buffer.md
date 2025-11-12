# Buffer

A buffer in is temporary storage that holds raw binary data. It's is a fixed-size chunk of memory allocated outside the V8 JavaScript engine's heap.

## Why Buffers Exist

JavaScript was originally designed for browsers and didn't have a way to handle binary data. Node.js needed to work with binary data (files, network streams, images, etc.), so Buffers were created to bridge this gap.

## `from()`

This method is used to create a buffer from a `string`, `array`, or another buffer. 

**Syntax**

```js
Buffer.from(data, encoding)
```

`encoding` is optional.

**Example**

```js
const buffer = Buffer.from("Hello, World!", 'utf8')
```

Here `utf8` is telling system to use 8 bits to represent each character code.

**How read a buffer back?**

```js
console.log(buffer.toString("utf8")) // Hello, World
```

## alloc

`Buffer.alloc()` in Node.js is used to **create a new buffer of a fixed size**, and it **initializes (fills)** the buffer with zeros for safety

**Syntax**

```js
Buffer.alloc(size[, fill[, encoding]])
```

**Parameters:**

- `size` → The length (in bytes) of the buffer you want.

- `fill` *(optional)* → Value to fill the buffer with. Default: `0`.

- `encoding` *(optional)* → Encoding if `fill` is a string (e.g., `'utf8'`, `'base64'`).

**Example**

Create a 10-byte buffer (filled with zeros)

```js
const buf = Buffer.alloc(10);
console.log(buf);
```

**How to write data in buffer, created using `alloc`?**

```js
buf.write("Asif")
console.log(buf)
```

## Concatenate Buffers

```js
const b1 = Buffer.from("Asif");
const b2 = Buffer.from(" Shahzad");
const fullNameBuffer = Buffer.concat([b1, b2]);
console.log(fullNameBuffer.toString());
```
