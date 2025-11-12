[Video Tutorial](https://youtu.be/AOPmqw9scfc?si=0E6a_d1KJDP5zRns)
JavaScript ke andar, prototype ek aisa inheritance mechanism hai jiske zariye objects ek dosre ke darmiyan properties aur methods ko share kar sakte hain.

Har object ke paas aik internal `__proto__` aik property hoti hey jo kisi dosray object jiski properties ham chatey k hamarey object mey honi chaye us object ko hamarey object ki prototype set karney kelye istemal hoti hey.

```js
let employee = {
  salary: null,
  calculateTax() {
    return this.salary - this.salary * 0.1;
  },
};

let asif = {};
asif.__proto__ = employee;
asif.salary = 100000;
console.log(asif.calculateTax());
```

Ye prototype kisi aur object ko point karta hai, is tarah ek chain banti hai jise "prototype chain" kehte hain. 

Ye chain tab tak chaltī hai jab tak kisi object ka prototype `null` na ho jaye — jo ke chain ka last link hota hai.

```js
let name = "Asif"
```

Abhi dekhne par ye sirf ek string lagti hai, lekin jaise hi aap `name.` ka use karte hain (dot operator ke zariye), aapko bohat saare methods aur properties nazar aati hain. Ye sab JavaScript ke prototype mechanism ki wajah se hi possible hota hai. 

```js
let name = "Asif"
name.__proto__
```

If you paste the code snippet give above in to the browser console you will see the prototype of name which is in this case the String class.

## How Manipulate Prototype?

For example meyray pass aik object hey 

```js
let user = {
  name: "Asif",
  greet: () => console.log("Hello, ", this.name)
}
```

Abh farz kiya mujeh aik or object banana hey to mey kis traha `user` object ko as a prototype  user kartey howay new `user2` object bana sakta hun.

```js
user2 = Object.create(user)
console.log(user2.__proto__)

// Output
> { name: 'Asif', greet: [Function: greet] }'
```

Abh mey yaha pay properties ko overide kar skta hun with object `user2`

```js
user2.name = "Asim"
```

Now yeah bina parent object ko change kiye sirf child object `user2` k name ko `Asim` set kar deyga.

```js
console.log(user.name) // Asif
console.log(user2.name) // Asim
```

Not recommended but you can directly make change in the protype object from the child object in this case the protype object is `user` :

```js
user2.__proto__.name = "Asim"
console.log(user.name) // Asim
```

## Prototype Chain

Her object ki prototype internally kisi dorsray object ko point kar rahi hoti hey untill k kisi object ki `__proto__` `null` k equal nahi ho jati jaha per chain break ho jati hey.

![[diagram-export-10-07-2025-12_15_30.svg]]

## Recommendations

Whenever you have to use any object as protype for any other object you can use this built-in syntax:

```js
let user = {
  name: "Asif",
  greet: () => console.log("Hello, ", this.name)

}

user2 = {}
user2 = Object.setPrototypeOf(user2, user)
console.log(Object.getPrototypeOf(user2));
```

**Breakdown**

Set the prototype of `user2` to as `user` object.

```js
user2 = Object.setPrototypeOf(user2, user)
```

To confirm you get the protype of any object:

```js
console.log(Object.getPrototypeOf(user2));
```

## 