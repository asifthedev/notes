## Callback Function

Callback wo function hota hai jo **dusre function ko argument ke tor par diya jata hai** aur wo baad me chalaya jata hai.  
**Example:**

```js
function greet(name, callback) {
  console.log("Hello " + name);
  callback(); // baad me chal raha function
}

function sayBye() {
  console.log("Goodbye!");
}

greet("Asif", sayBye);
```

Output:

```
Hello Asif
Goodbye!
```

### **2. Higher-Order Function (HOF)**

Higher-order function wo hota hai jo:

1. Function ko **argument** ke tor par leta hai  
   **ya**

2. Function ko **return** karta hai.

Example:

```js
function calculate(num, operation) {
  return operation(num);
}

function double(x) {
  return x * 2;
}

console.log(calculate(5, double)); // 10
```

`calculate` ek higher-order function hai, kyun ke ye dusra function (`double`) as argument le raha hai.

---

### **Short samajh lo:**

- **Callback** = Jo function dusre function ke andar **baad me call** hota hai.

- **Higher-Order Function** = Jo function dusre function ko **as input ya output** use kare.


