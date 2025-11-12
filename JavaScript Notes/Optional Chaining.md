## Optional Chaining

Optional Chaining ek JavaScript feature hai jo nested object properties safely access karne ke liye use hota hai. Agar beech ka koi property null ya undefined ho, toh error throw karne ke bajaye yeh undefined return karta hai. Isse humein har step pe multiple null checks likhne ki zarurat nahi padti aur code clean aur readable ban jata hai

```js
let user = {
  name: "Ali",
  address: {
    city: "Lahore",
    zip: "54000"
 }
}

// let user = null

console.log(user?.address?.city ?? "Unknown")
```

Before this feature, if you had a deep nested object structure and wanted to access a property, you had to perform multiple checks to ensure that each level in the chain was not `null` or `undefined`.

Without these checks, attempting to access a property on a `null` or `undefined` value would throw a `TypeError`. This led to code that was cluttered with repetitive `&&` checks, making it harder to read and maintain

```js
let user = {
  name: "Ali",
  address: {
    city: "Lahore",
    zip: "54000"
  }
};

// ✅ Safe code likhna padta tha:
let city;

if (user && user.address && user.address.city) {
  city = user.address.city;
} else {
  city = "Unknown";
}

console.log(city); // "Lahore"
```

### Optional Chaining with Method

```js
let user = {
    gree() {
        return "Hi, Asif";
    }
}

console.log(user.gree?.());
```
