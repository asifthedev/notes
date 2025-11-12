## Node JS

Nodejs is Javascript runtime environment that lets you run Javascript outside of the browser on your local machine. It has JavaScript V8 engine embedded in it and some C++ code.

It has been made by Riyan.

## Module in Node JS

Node JS mey har file ko aik module consider kia jata hey ja bhi koee file run hoti hey to usay **Module Wraper Functions** mey wrap kar k run kia jata hey

**Return Type**

Yeah function`module.export` ko retrun karta hey

```js
(function (exports, require, module, __filename, __dirname) {

return exports;
});
```

## exports

Node.js me har file ek **module** hoti hai.  Us module ke andar ek **object** hota hai:

`module.exports = {};`

Aur Node automatically ek **shortcut variable** banata hai jiska naam hota hai `exports`,  
jo initially **usi object ko point karta hai**

```js
exports === module.exports  // true at start
```

## require

Kisi bhi file ko require function isi Module Wrapper Function k zariye say provide kia jata hey 

Yeah function kisi bhi js file ka path as a string layta hey or uska code execute karta hey yeah module ka code bhi wrapper function k ander daal k hi execute kia jata hey or phir yeah function `module.export` object ko return karta hey, jo phir `require()` function wapis return kar deyta hey jaha pay yeah call huwa hey

## module

yeah object current module k barey mey meta information provide karta hey or most importantly `module.export` is object mey hota hey. 

You can print this object:-

```js
console.log(module)
```

**Output:-**

```js
{
  id: '.',
  path: 'C:\\Users\\mrasi\\Downloads\\whiteboard',
  exports: {},
  filename: 'C:\\Users\\mrasi\\Downloads\\whiteboard\\app.js',
  loaded: false,
  children: [],
  paths: [
    'C:\\Users\\mrasi\\Downloads\\whiteboard\\node_modules',
    'C:\\Users\\mrasi\\Downloads\\node_modules',
    'C:\\Users\\mrasi\\node_modules',
    'C:\\Users\\node_modules',
    'C:\\node_modules'
  ],
  [Symbol(kIsMainSymbol)]: true,
  [Symbol(kIsCachedByESMLoader)]: false,
  [Symbol(kURL)]: undefined,
  [Symbol(kFormat)]: undefined,
  [Symbol(kIsExecuting)]: true
}
```

## __filename

Absolute path of the module or current file.

```js
console.log(__filename)
// C:\Users\mrasi\Downloads\whiteboard\app.js
```

## __dirname

```js
console.log(__dirname)
// C:\Users\mrasi\Downloads\whiteboard
```

## Type of Module in Node JS

1. Builtin Module (Jo by default node mey ship hotey heyn e.g. `fs`)

2. 3rd Party Module (Jo app npm k zariye say download kartey ho)

3. Custome Module (App apna custome likha huwa code)

## What is npm?

**NPM** stands for **Node Package Manager**.  
It is a **tool that helps you install, manage, and share packages (libraries or modules)** for JavaScript and Node.js projects.

## What is `package.json`?

Yeah apke project ki configurations ko contain karta hey. Ismey apke project ka name version script or array of all the third party dependencies you have installed using npm.

## What is `package-lock.json`?

It keep tracks of dependenceis of dependencies. Dependencies bhi aagey or dependencies pay depend kar rahi hoti heyn to unka track rakhney kelye hoti hey package.lock.json
