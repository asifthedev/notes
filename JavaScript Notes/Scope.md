# Scope

An area or a range in which variables, functions, and objects are accessible to other parts of the code. There are four kinds of scopes in JavaScript:-

1. Global Scop

2. Block Scop

3. Functional Scop

4. Lexical Scop

## Global Scope

A scope in which a variable, function, and object is accessible anywhere in the code; in other words, it's not restricted to a particular block of code.

## Block Scope

A block means the area between two curly braces `{}`, the variable function and objects declared and defined inside a block are only accessible in this block.

**Exception:** `var` is not restricted to block scope; it can also be accessed outside a block

## Functional Scope

`var`, `let`, `const` agar function k andar declare hain to sirf usi function me accessible hain.

## Lexical Scop

Variables ka scope unki **code me physical position (source code structure)** per decide hota hai, na k runtime execution per.

Agar aap ek function ke andar variable declare karte ho, to woh sirf us function aur uske nested (andar wale) functions ko hi accessible hoga. Bahar ke functions ya global scope use access nahi kar sakte.

```js
function outer() {
  let name = "Asif"; // outer scope

  function inner() {
    console.log(name); // inner function ko "name" access hai
  }

  inner();
}

outer(); // Output: Asif

```

Yahan `inner()` function ke paas apne scope ke saath-saath outer scope (`outer()` ka variable `name`) ki bhi access hai.  
Isko **lexical scoping** ya **scope chaining** kehte hain.


