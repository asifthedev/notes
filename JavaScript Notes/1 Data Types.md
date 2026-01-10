There are two types of datatypes in JavaScript

1. Primitive
2. Non-Primitive

## Primitive

Primitive data types in **JavaScript** woh data types hote hain jo **basic aur immutable (change na hone wale)** hote hain. 

### Number

Represents both integers and floating-point numbers, and can also include the special values `Infinity`, `-Infinity`, and `NaN` (Not-a-Number).

```js
let age = 32;
const pi = 3.14;
let likes = infinity;
let num = NaN;
```

### Bigint

 A special numeric type for representing whole numbers larger than the limit of the `Number` type. A `BigInt` is created by appending `n` to the end of an integer

```js
let views = 1324242312104832n
let likes = BigInt("13142331212434")
```

### String

Used for textual data and enclosed in single quotes, double quotes, or backticks (for template literals).

```js
let name = "Asif"
let desigantion = 'Sales'
let income = `12345432`
```

### Boolean

A logical type that can only have one of two values: `true` or `false`. These are often used in conditional statements.

```js
let isStatment = true;
```

### Undefined

Represents a variable that has been declared but has not yet been assigned a value.

```js
let num = undefined;
let age; // undefined 
```

### Null

Used to represent an intentional absence of any object value. Unlike `undefined`, it must be explicitly assigned.

```js
let emptyValue = null;
```

### Symbol

A unique and immutable primitive value often used as a unique identifier for object properties to avoid naming conflicts.

```js
let a = Symbol("a")
let b = Symbol("a")
console.log(a === b);
```

## Non Primitive

A non primitive data type does not holds data value instead it stores reference to the memory location where the data is actually stored. Non primitive data types are immutable. 

The primary non primitive data type is `object`.  There are three type of object or non primitive data types are Array, Object, Function.
