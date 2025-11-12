**What if the number of arguments is unknown?**
Well, in this scenario we can use rest operator that will bundle variable number of arguments into array object.

```js
function cart(...all) {
  return all;
}

console.log(cart(100, 200, 50));
```