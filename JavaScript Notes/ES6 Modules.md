# **ES6 Modules**

Yeah feature say ham aik file mey likhey howay code dosri js file mey access ya use kar saktey heyn jisay code moduler or resuable ho jata hey. Isay pehlay CommonJS wala syntax use hota hey `required()` function k sath.

## Export Keyword

It's used to mention which particular piece of code you want to share with other modules and JavaScript files. There are two types of export:-

1. Named Export

2. Default Export

### Named Export

Ismey ham specifically export honey waley variable, object, ya function k exact name ko mention kartey heyn jo `{}` k ander enclosed hota hey.

```js
let user = {name: 'asif', age: 23}
export {use}
```

**Multiple named exports**

App multiple variables, objects, ya functions ko bhi expot kar saktey heyn:-

```js
let user = {name: 'asif', age: 23}
let isLogedIn = true
export {user, isLogedIn}
```

**Renaming**

You can rename your actual variable, object, or function while exporting it using the `as` keyword.

```js
let user = {name: 'asif', age: 23}
let isLogedIn = true
export {user as userObject, isLogedIn as loginFlag}
```

## Default Export

The difference between named and default export is that you don't need any particular name to access a variable, function, or object from another module or JavaScript file. 

```js
// utilities.js
export default function greet(name){
    console.log(`Hell, ${name}`)
}
```

**Importing:-**

Import karte waqt **naam apni marzi ka rakh sakte ho**, curly braces `{}` ki zaroorat nahi hoti.

```js
import anyName from './utilities.js'
```

Ek file me **sirf ek default export** hota hai, lekin **multiple named exports** ho sakte hain.

## Import Statement

It's used to import code from other modules or JavaScript files.

**Importing Named Export**

```js
import { user } from './users.js'
```

**Note:** file k name k sath `.js` laga zrori hota hey node js mey

**Renaming while importing**

```js
import {user as userObject} from './users.js'
```
