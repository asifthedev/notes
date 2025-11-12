Hoisting in JavaScript is a behavior where declarations of variables (declared with `var`), functions, and classes are conceptually "moved" to the top of their respective scopes during the compilation phase, before the code is executed. This means you can use these elements before their actual declaration in the code. 

```js
console.log(n);
var n = 10;
```

Now before execution the declaration will be moved to the top of the respective scop of n in this case it's Global Scop. 

![[hoisting.svg]]
### 💡 **Hoisting kya hota hai?**

**Hoisting JavaScript ka aik behavior hai** jisme:

> JavaScript pehlay code ko **run** karne se pehlay, **variable declarations** (e.g. `var`), **function declarations**, aur kuch had tak **classes** ko unke **scope ke top par le jata hai**.

Matlab:

> Tum likhtay ho code neeche, **JavaScript usko pehlay upar le jata hai** (sirf declaration ko, value ko nahi).

---

### ✅ Example 1: `var` ke sath hoisting

```javascript
console.log(x); // Output: undefined
var x = 5;
```

**Explanation:**

JavaScript isko pehlay aise samjhta hai:

```javascript
var x;         // hoisted declaration
console.log(x); // undefined
x = 5;         // initialization
```

> Dekha? `var x` upar chala gaya, **lekin value assign nahi hui** jab tak actual line na aaye.

---

### ❌ `let` aur `const` ke sath hoisting hoti hai **lekin different**

```javascript
console.log(y); // ❌ Error: Cannot access 'y' before initialization
let y = 10;
```

> Yahan bhi `let y` technically hoist hua hota hai, **lekin JavaScript usay use nahi karne deti** jab tak uski line nahi aati. Isay **Temporal Dead Zone (TDZ)** kehtay hain.

---

### ✅ Function declaration ka hoisting:

```javascript
greet(); // Output: Hello

function greet() {
  console.log("Hello");
}
```

> Poora function upar chala jata hai — tum usay pehlay bhi call kar saktay ho.

---

### ❌ Function expression ka hoisting nahi hota:

```javascript
sayHi(); // ❌ Error: sayHi is not a function

var sayHi = function () {
  console.log("Hi");
};
```

**Explanation:**

JavaScript isko aise dekhta hai:

```javascript
var sayHi; // hoisted as undefined
sayHi();   // Error: undefined is not a function
sayHi = function () { ... };
```

---

### 📌 Summary (Asaan Urdu mein):

|JavaScript cheez|Hoist hoti hai?|Use pehlay kar saktay ho?|
|---|---|---|
|`var`|✅ Yes|⚠️ Sirf "undefined" milega|
|`let` / `const`|✅ Yes|❌ Error deta hai (TDZ)|
|Function declaration|✅ Yes|✅ Bilkul|
|Function expression|❌ Nahin|❌ Error deta hai|

---

Agar chaho to mai **visual diagram** bhi bana kar samjha sakta hoon. Bolo agar chahiye.