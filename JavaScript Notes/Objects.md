## What is an Object?

An object is a collection of key-value pairs. It's used to represent real-world entities in Javascript.

```js
let user = {name: "Asif", age: 22}
```

**Destructuring Object**
Object destructuring in JavaScript is a powerful feature that allows for extracting properties from objects and binding them to variables. This simplifies code by reducing the need to access properties using dot notation repeatedly.

**Basic Extraction:** You can extract properties by matching the variable names to the object's property keys.

```js
const person = {
firstName: 'John',
lastName: 'Doe',
age: 30
};

const { firstName, age } = person;

console.log(firstName); // Output: John
console.log(age);      // Output: 30
```

**Renaming Variables:** You can assign a different variable name to an extracted property using a colon.

```js
const product = { id: 123, description: 'Laptop' };
const { id: productId, description: productDescription } = product;
console.log(productId);       // Output: 123
console.log(productDescription); // Output: Laptop
```

**Default Values:** You can provide default values for properties that might not exist in the object, preventing `undefined`.

```js
const settings = { theme: 'dark' };
const { theme, fontSize = 16 } = settings;
console.log(theme);    // Output: dark
console.log(fontSize); // Output: 16
```

**Nested Destructuring:** You can extract properties from nested objects by mirroring the object's structure within the destructuring assignment.

```js
const data = { user: { name: 'Bob', email: 'bob@example.com' } };
const { user: { name, email } } = data;
console.log(name);  // Output: Bob
console.log(email); // Output: bob@example.com
```

**Rest Property:** The rest property `...` can be used to collect remaining properties into a new object.

```js
const person = { firstName: 'Jane', lastName: 'Doe', occupation: 'Engineer' };
const { firstName, ...rest } = person;
console.log(firstName); // Output: Jane
console.log(rest);      // Output: { lastName: 'Doe', occupation: 'Engineer' }
```

**Function Parameters:** Object destructuring is commonly used in function parameters to directly access specific properties of an object passed as an argument.

```js
function displayUser({ name, age }) {
  console.log(`Name: ${name}, Age: ${age}`);
}
const newUser = { name: 'Charlie', age: 25 };
displayUser(newUser); // Output: Name: Charlie, Age: 25
```

Object destructuring enhances code readability and conciseness, particularly when dealing with data from APIs, configuration objects, or complex data structures. 

## What is an Object?

An object is a collection of key-value pairs. It's used to represent real-world entities in JavaScript. Keys hamesha string ya symbol hoti hain, values kuch bhi ho sakti hain (number, string, function, array, dusra object).

### How to create an object?

**Object literal way of creating an object**

```js
let user = {name: "Asif", age: 22}
```

**Constructor Function to Create an Object**

```js
function User(username) {
  this.username = username;
}

let u1 = new User("asifshahzad");
```

**new Object() constructor**

```js
let user = new Object({ name: "Asif" });
```

**Using class syntax**

```js
class User {
  constructor(username, email, password) {
    this.username = username
    this.email = email
    this.password = password
  }
}

let u1 = new User('asif', 'info@asifshahzad.me', '123')
```

**Object.create()**

`Object.create(proto)` ek **naya object banata hai** jiska **prototype** aap manually decide karte ho.

```js
let human = { name: "asif", age: 22 };
let user = Object.create(human);
```

The above code is doing this behind the scenes:

```js
let human = { name: "asif", age: 22 };
let user = {};
user.__proto__ = human;
console.log(user.name);
```

## How to set a symbol as a key for a value?

```js
let id = Symbol("id");
let user = { username: "Asif", [id]: 123 };
console.log(user);  // { username: 'Asif', [Symbol(id)]: 123 }
console.log(user[id]) // 123
```

## What is Object.freeze()?

Yeah aik static method hey jo object ko read only bana deyta hey na app usko modifying kar patey or na hi koee key delete or add kar patey ho.

```js
let human = { name: "asif", age: 22 };
Object.freeze(human);
human.name = "Asim";
console.log(human);
```

### What is Object.assigne()?

Yeah, multiple source objects ki enumerable properties ko target object mey merge ya copy karney kelye use hota hey.  Yeah, shallow copy banata hey.

```js
let user = { name: "Asif", age: 22 };
let userMetadata = { logedIn: true, preferences: ["movies", "animals"] };
let userFull = Object.assign({}, user, userMetadata);
console.log(userFull);

/*
{
  name: 'Asif',
  age: 22,
  loggedIn: true,
  preferences: [ 'movies', 'animals' ]
}
*/
```

### Object.keys()

Aik static method hey Object class ka, or object ki keys ko aik array mey return karta hey

**Syntax**

```js
Object.keys(object)
```

**Example:**

```js
let user = { name: "Asif", age: 22 };
console.log(Object.keys(user)); // [ 'name', 'age' ]
```

### Object.values()

A static method that takes an object as an input and returns the values of the keys of an object.

```js
let user = { name: "Asif", age: 22 };
console.log(Object.values(user)); // [ 'Asif', 22 ]
```

### Object.entries()

Aik nested array return karta hey jismey har key or value aik seprate array hota hey

```js
let user = { name: "Asif", age: 22 };
console.log(Object.entries(user)); // [ [ 'name', 'Asif' ], [ 'age', 22 ] ]
```

### How do you check a property is present in the object or not?

```js
let user = { name: "Asif", age: 22 };
console.log(Object.hasOwn(user, "name"));
```

# 