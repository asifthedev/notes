## Variable Declaration 

**var**

It's function scoped which mean it's accessible anywhere in the direct parent function.
```javascript
function testScope() {
  if (true) {
    var a = 1;
    let b = 2;
  }
  console.log(a); // 1 (accessible)
  console.log(b); // ReferenceError: b is not defined
}
testScope();
```
It also allow for redeclaration redeclaration:
```js
var name = "Asif"
var name = "Asim"
console.log(name) // Asim
```

**let**
It's blocked scop which mean it is only accessible withing it's block enclosed in curly braces.
```javascript
if(true){
   let b = 3;
}
console.log(b) // ReferenceError: b is not defined
```

**const**
It's used to create constant variable, a type variable you can not change it's value once it's assigned.
```js
const pi = 3.14;
pi = 1.2; // TypeError: Assignment to constant variable.
console.log(pi);
```

[Refer to this video tutorial for better understanding](https://youtu.be/NNjQFqgF3sk?si=qAOl3UaRFsN3GT_Z)