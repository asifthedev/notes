## Constructor Functions

Old ES6 mey constructor functions ko use kia jata thaa object ko create or initialize karney mey, classes k aney say pehlay.

```js
## Class

It is a blueprint for creating objects with similar properties and methods. Classes let you simulate real-world entities or objects (their properties and behaviors) in programming.

Jab bhi hamey aik tarah k boht sarey objects k barey mey data store karwana hota hey to instead k ham objects kelye baat uski properties or methods ko define karey. Ham aik hi dafa class bana deytay heyn jo k aik blueprint k tor per kaam karti or isay ham naye objects ko banatey heyn.

```js
class Car {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }
  start() {
    console.log("start");
  }
  stop() {
    console.log("stop");
  }
}
```

### Constructor

Constructor class k ander likha janey wala aik esa function hota hey, jo automatically call invoke ho jata, jesay hi app koee naya banate ho.

**Key Points:**

1. Ek class me **sirf ek constructor** hota hai.

2. Agar aap constructor nahi likhte, to JavaScript ek **default empty constructor** bana leta hai.

3. Constructor ka naam **hamesha `constructor` hi hota hai**.

4. Ye `new` ke bina automatically run nahi hota.

## Object

It's an instance of a class that represents a specific object.

```js
class Car {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }
}

let toyota = new Car('Toyota', 'Fortuner') // Object creation
```

## Inheritance

Jab aik class kisi dosri class ki properties ko inherit kar leyti hey to isay inheritance boltey heyn.  Jismey jo class inherit kar rahi hey woh child class or jisay ho rahi heyn woh parent class kahlati hey.

```js
class Vehicle {
  constructor(brand, model) {
    this.brand = brand;
    this.model = model;
  }
}

class Car extends Vehicle {
  constructor(brand, model) {
    super(brand, model);
  }
}

let c1 = new Car("Toyota", "Fortuner");
console.log(c1.brand);
```

## Main Reasons Why `super` is Used

### 1. **To call the parent class constructor**

When you define a constructor in a child class, you **must** call `super()` before using `this`, because it initializes the parent’s properties.

```js
class Human {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

class Teacher extends Human {
  constructor(name, age, subject) {
    super(name, age);   // calls Human’s constructor
    this.subject = subject;
  }
}

let t = new Teacher("Asif", 25, "Math");
console.log(t); 
// Teacher { name: "Asif", age: 25, subject: "Math" }
```

Without `super(name, age)`, you can’t set `name` and `age` because `this` won’t be initialized.

---

### 2. **To call parent class methods**

Sometimes the child class overrides a method, but you still want to use the parent’s method inside it. That’s where `super.methodName()` is used.

```js
class Human {
  eat() {
    console.log("Human eats food");
  }
}

class Teacher extends Human {
  eat() {
    super.eat();        // calls parent’s eat()
    console.log("Teacher eats quickly during break");
  }
}

let t = new Teacher();
t.eat();
// Output:
// Human eats food
// Teacher eats quickly during break
```

---

### 3. **Behind the scenes default**

If you don’t write a constructor in the child class, JavaScript automatically adds this for you:

```js
constructor(...args) {
  super(...args);
}
```

That’s why in your earlier example, `Teacher` worked fine without explicitly writing `super()`.

---

## Summary

- `super()` → calls parent constructor (must be called before using `this` in a child constructor).

- `super.methodName()` → calls a method from the parent class.

- If you don’t define a constructor in the child, JS inserts one with `super(...args)` automatically
