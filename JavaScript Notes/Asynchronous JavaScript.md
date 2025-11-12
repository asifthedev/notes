## Synchronous Execution

Code jis sequence mey likha hey usi sequence mey line by line execute hota hey har line apney apney say pehlay likhi hoee line ya instruction k execute honey ka wait karti hey.

**Example**

```js
console.log('One')
console.log('Two')
console.log('Three')
```

### Cons

Ager koee instruction ziyada time lay rahi hey to control wahi stuck ho jata hey or execution flow block ho jata hey, or baad mey likhi hoee instruction ko wait karna parta.

## Asynchronous

Asynchronous programming in JavaScript allows us to execute tasks **concurrently** without blocking the execution of specific instructions. 

If a task is **time-consuming** (like fetching data from a server or reading a file), we can let it run in the **background**, while the rest of the code continues executing. 

Once the background task is complete, its result is handled through **callbacks, promises, or async/await**, ensuring smooth and non-blocking execution.

## Callback Function

Jab ham kis function ko as input pass kartey heyn kisi dosray function ko jo isay baad mey mostly end per call kar deyta hey, isay callback function boltey heyn.

## Callback Hell

Jab multiple nested callback aik dosray k uper stack ho jatey heyn jisay code understand karna or error tracking mushkil ho jati hey to isay kehtay callback hell.

## Promises

A **Promise** in JavaScript is an object that represents the eventual **completion (success)** or **failure (error)** of an asynchronous operation.

A Promise has **3 states**:

1. **Pending** → Initial state (operation still in progress).

2. **Fulfilled** → The operation completed successfully (`.then()` handles this).

3. **Rejected** → The operation failed (`.catch()` handles this).

```js
let promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Data received!"); // success
    // reject("Something went wrong"); // failure
  }, 2000);
});

promise
  .then(result => console.log(result))  // runs if resolved
  .catch(error => console.error(error)); // runs if rejected
```

In short: **A Promise is a cleaner way to handle async tasks without blocking the main thread.**

#### What is mean by seatling

## Promise Chaining

**Promise chaining** means calling multiple `.then()` methods one after another, where the output (resolved value) of one `.then()` is passed as the input to the next.

```js
new Promise((resolve, reject) => {
  setTimeout(() => resolve(10), 1000); // step 1
})
.then(result => {
  console.log("First result:", result);
  return result * 2; // pass to next .then
})
.then(result => {
  console.log("Second result:", result);
  return result + 5; // pass to next .then
})
.then(result => {
  console.log("Final result:", result);
});
```

Key Points:

- Each `.then()` returns a **new promise**, which allows chaining.

- If you return a value, it goes to the next `.then()`.

- If you return a promise, the chain waits for it to resolve before continuing.

- `.catch()` at the end handles any error in the chain.

# Async Await

Yeah promises ya asynchronous operation ko syncronously handle karney ka sab say clean and intuitive tarika hey.

## Async

Async keyword aik asyncronous function declare karney kelye use hota hey jo hamesha aik promis return karta hey, ager app nahi kartey JavaScript implicitly khud say returning value ko promise mey wrap kar deyti hey.

## Await

The `await` keyword in JavaScript is used to pause the execution of an `async` function until a Promise settles (either resolves or rejects) and returns its result.

**NOTE:** It can only be used inside functions declared with the `async` keyword.

Here's a breakdown of how `await` works:

- **Pauses Execution:** 
  
  When `await` is placed before an expression that returns a Promise, it effectively pauses the execution of the `async` function at that point.

- **Waits for Promise Resolution:** 
  
  The function remains paused until the awaited Promise resolves (successfully completes) or rejects (encounters an error).

- **Returns Resolved Value:** 
  
  If the Promise resolves, `await` returns the resolved value, allowing you to assign it to a variable and continue with the function's logic as if it were synchronous code.

- **Handles Rejections:** 
  
  If the Promise rejects, `await` will throw an error, which can be caught using a `try...catch` block within the `async` function.

- **Improved Readability:** 
  
  `await` simplifies asynchronous code by allowing you to write it in a more sequential, synchronous-like style, making it easier to read and understand compared to using `.then()` chains.
