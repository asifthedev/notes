[Video Tutorial](https://youtu.be/gPKzwAORly8?si=7puwqDSBp56Ll-HN)
When the JavaScript engine scans a script file, it makes an environment called the **Execution Context** that handles the entire transformation and execution of the code. There are two types of execution contexts: **global** and **function**.
## Global Execution Context

The global execution context is created when a JavaScript script first starts to run, and it represents the global scope in JavaScript.

**The Global Execution Context (GEC)** is the environment where JavaScript code that is not inside any function gets executed. It sets up the global object (`window` in browsers, `global` in Node.js), and the `this` keyword.

## Phases of Execution Context

There are two phases of an Execution Context the Creation Phase and Execution Phase.

**Creation Phase**
In this phase the variable and functions are loaded into memory where each variable assigned with an `undefined` value by default and functions definition is loaded into memory. 

```js
var n = 5;

function square(n) {
  let answer = n * n;
  return answer;
}

let nSquare = square(n);
```

Here's how this code executes in the memory.
  
![[EC.svg]]

## Functional Execution Context
For every function in there's a separate local functional context has been made and it also have two phases as GEC. As you can see on the above the image.