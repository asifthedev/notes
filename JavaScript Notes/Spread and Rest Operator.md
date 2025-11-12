# Spread and Rest Operator

Based on the use case, this `...` triple dotted notation is called the spread or rest operator.

## Spread Operator

Spread operator (`...`) ka use arrays ya objects ko expand karne k liye hota hai. Matlab ek array/object k elements ko tod k alag alag values ki tarah use karna.

```js
let arr1 = [1, 2];
let arr2 = [3, 4];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4]
```

## Rest Operator

Rest operator (`...`) ka use multiple arguments ya properties ko ikatha karne k liye hota hai. Matlab jitni bachi values hain, unko ek array ya object me collect kar leta hai.

```js
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
console.log(sum(1, 2, 3)); // 6
```
