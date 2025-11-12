### Constructor Function

Classes aney say pehlay old Ecma Script mey yeah Constructor Functions use hotey they objects ko create or initialize karney kelye. 

A **constructor function** works like a **blueprint** or **factory** to create objects.  
Objects created with it contain the same properties (and can share methods via prototype).

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

let student = new Person("Asif", 21);
```

Here:

- `Person` is the **constructor function**.

- `student` is an object created using `new Person(...)`.

---

### Prototype in Constructor Function

Every function in JavaScript automatically has a property called **`prototype`**.

- `Person.prototype` is an object.

- Any object created with `new Person()` will have its `__proto__` linked to `Person.prototype`.

```js
function Animal(name) {
  this.name = name;
}

let cat = new Animal("cat");

console.log(cat.__proto__ === Animal.prototype); // true
```

So:

- `Animal.prototype` = the shared object (blueprint’s shared space).

- `cat.__proto__` = the internal link from the instance to that shared object.

### Adding Methods via Prototype

Instead of putting methods inside the constructor (which would create **copies** for each object),  
we can attach methods to the prototype so **all objects share them**.

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function () {
  console.log("Hello, my name is " + this.name);
};
```

### Example in Action

```js
const asif = new Person("Asif", 30);
const ali = new Person("Ali", 25);

asif.sayHello(); // Hello, my name is Asif
ali.sayHello();  // Hello, my name is Ali
```

Notice:

- Neither `asif` nor `ali` has `sayHello` inside them directly.

- They **look it up** in `Person.prototype` through their `__proto__`.

### Analogy

Think of `Person.prototype` as a **library** of shared behaviors.  
Every new person (`asif`, `ali`) doesn’t carry their own copy of the books — they just have a **membership card (`__proto__`)** pointing to the same library.