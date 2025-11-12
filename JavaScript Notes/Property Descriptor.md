## Property Descriptor

Yeah kis bhi object ki properties ko configure karney kelye istemal hota hey  jesa k woh enumrable hey usay change ya delete kia ja sakta hey ya nahi isko define karney kelye use hotey heyn.

## defineProperties()

Yeah function multiple properties keylye properties descriptors ko set karney kelye istemal hota hey

```js
let user = {}

Object.defineProperties(user, {
    name: {
        value: "Asif Shahzad",
        enumerable: true,
        writable: true,
        configurable: true
    }
})

console.log(user.name); // 'Asif Shahzad' 
```

**NOTE** `defineProperties()` method mey by defualt sab descriptors ki value false hoti hey, to jab tak app true nahi kartey explicitly tabh tak app na to property ko dell, modify or loop kar saktey.

**enumrable**

Keys ko loop kia ja skata hey (`for...in` or `Object.keys()`) ager enumerable true hey to object ki keys ko loop kia ja sakey hey  ager kisi key ka enumerate descriptor false hey to woh key na to loop ho sakti na hi Object.keys() method mey woh key show hogi

**writable**

value ko modify kia ja sakta hey (`true`) ya nahi (`false`)

**configurable** 

object ki kisi property ko delete kia ja sakta (`true`) hey ya nahi (`false`)

**value**

proper ki value ko define karney kelye use hota hey
