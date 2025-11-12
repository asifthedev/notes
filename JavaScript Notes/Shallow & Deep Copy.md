It only copy the top level or element at first level but nested elements inside array or object are referenced. The problem with the shallow copy is any change in referenced element will also change the element in original object or array that is why It's not the true copy. 

**Shallow Copy of an Array**

```js
let arr1 = [1, [2, 3]]
let arr2 = [...arr1]

arr2[1][0] = 99 // arr1 = [1, [99, 3]] 
```

**Shallow Copy of an Object**

```js
let obj1 = { name: "Asif", hobbies: ["reading", "font collection"] };
let obj2 = { ...obj1 }; // shallow copy

obj2.hobbies[1] = "watching movies"; // this will change the value in obj1 as well
console.log(obj1); // { name: 'Asif', hobbies: [ 'reading', 'watching movies' ] }

// // OR you can make shallow copy using

// obj2 = Object.assign({}, obj1); // target -> {}, source -> obj1
```

## Deep Copy

A deep copy is true copy of an object in JavaScript. It actually copies elements of an object even nested one instead of creating reference to them like shallow copy.

**Deep Copy of an Array**

```js
arr1 = [1, [2, 3]];
arr2 = structuredClone(arr1);
arr2[1][0] = 99;
console.log(arr1); // [1, [2, 3]]
console.log(arr2); // [1, [99, 3]]
```

**Deep Copy of an Object**

```js
user1 = {
    name: "Asif",
    age: 32,
    hobbies: ["coding", "reading", "gaming"],
}

user2 = structuredClone(user1);
user2.hobbies[0] = "writing";
console.log(user1.hobbies); // ["coding", "reading", "gaming"]
console.log(user2.hobbies); // ["writing", "reading", "gaming"]
```