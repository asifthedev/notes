# New Operator

Sabh say pehlay baat kartey heyn `new` operator with **constructor function**. Ham sab say pehlay this ka behavior study kartey heyn constructor function k sath.

```js
function Human(name, age) {
  this.name = name;
  this.age = age;
}

let obj = new Human("Asif", 22);
console.log(obj); //Human { name: 'Asif', age: 22 }
```

1. Hamey aik object type milli

2. Object ki har property ya key ki value hamari passed value k equal set hey

**Ager Constructor Function Kuxh Return Karta Hey To**

```js
function Human(name, age) {
  this.name = name;
  this.age = age;

  return { gender: "male", height: 5.4 };
}

let obj = new Human("Asif", 22);
console.log(obj); // { gender: 'male', height: 5.4 }
```

Observations:

1. Ager ham CF say kuxh return karegay to constructor function wali properties k sath object millney k bajaye returned object as an output millay ga. 

**Ager Constructor Function Say Object K illawa kuxh return kartey heyn to**

```js
function Human(name, age) {
  this.name = name;
  this.age = age;

  return "I'm a primitive value";
}

let obj = new Human("Asif", 22);
console.log(obj); // Human { name: 'Asif', age: 22 }
```

**Observation:**

Ager ham constructor function say koee primitive value return kartey heyn to woh ignore kar di jati hey or badlay mey aik object milta un vaules k sath jo constructor ko function ko ham ney pass ki hey.

## The new operator

It does foure things:-

```js
function Human(name, age) {
  this.name = name;
  this.age = age;
}

// step 01
let obj = {};

// step 02
obj.__proto__ = Human.prototype;

// step 03
let result = Human.apply(obj, ["Asif", 32]);

// step 04
typeof result == "object" && result !== null ? result : obj;}
```
