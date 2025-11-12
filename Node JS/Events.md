# Events

Node JS event driven architecture follow karta hey. Yani bajaye iskey k kisi operation k complete honey ka wait kiya jaye Node JS jaise hi koi event hota hai (for example: file read ho gayi, request aayi, timer complete hua) to us event se attached **callback function** ko execute kar deyta hey.

The builtin `events` module node js mey use hota hey, hey events ko handle karney kelye.

```js
const EventEmitter = require("node:events")
```

Events module Event Emitter class retrun karta hey jisay ham new events ko create or listen kar saktey heyn.

```js
const emitter = new EventEmitter()
```

Now using the emitter object we can call `emit` method to raise an event. Let say we want an event to be raised as a new user join the chat group.

```js
emitter.emit("join", user)
```

Now we are passing the event name for sacke of lister to recognize this event later and name of the user that will be passed to callback function or listner as a paramerter for notigying the specifying which user has joined the chat.

This is how we can attach a listener to this `join` event:-

```js
emitter.on('join', (username) => {
    console.log(`${username}, has joined the chat!`)
})

emitter.emit("join", 'Asif') // Asif, has joined the chat!
emitter.emit("join", 'Asim') // Asim, has joined the chat! 
```

Events are multi callable objects, so any time an event with the name `join` will occur this listener handling the `join` event will be executed.

**Attaching multiple listerner to respond to one single event**

```js
const EventEmitter = require("node:events");

const emitter = new EventEmitter();

emitter.on("join", (username) => {
  console.log(`${username}, has joined the chat!`);
});

emitter.on("join", (username) => {
  console.log(`Say hello to ${username}!`);
});

emitter.emit("join", "Asif"); 
```

Here the event which is emitted on execution is `join` but in response two callbacks are executed.

## How to check the number of listeners attached with an event?

Let's check the number of litener for `join` event .

```js
const count = emitter.listenerCount("join") // 2
```

## How to grab the references of the listerner functions attached with an event?

```js
console.log(emitter.listeners("join"));
// [ [Function (anonymous)], [Function (anonymous)] ]
```

## How to remove a specific listener from an event?

```js
const EventEmitter = require("node:events");

const emitter = new EventEmitter();

const listenerOne = (username) => {
  console.log(`${username}, has joined the chat!`);
};

const listenerTwo = (username) => {
  console.log(`Say hello to ${username}!`);
};

emitter.on("join", listenerOne);
emitter.on("join", listenerTwo)

emitter.emit("join", "Asif"); 
```

Now let say we want to remove the `listenerOne` from `join` event:-

```js
emitter.on("join", listenerOne);
emitter.removeListener('join', listenerOne)

emitter.on("join", listenerOne);
```

The `removeListener(eventName, litener)` use kia hey. Axah yaha per aik cheez yaad rahey k app arrow function jo direct as a callback pass kiya huwa hey `on` function mey woh remove nahi hoga, qn k apko `removeListener` mey listener function ka memory reference pass karna parta hey.

Becuase aik listener mey mutiple listener jo direct as callback pass kiye gey heyn `on` function mey ho saktey ho to kesay pata chalay ga k konsa wala listener hata hey. To is liye hamey elehda say listener function define karna parey ga.

## How to remove all listener attached with an event?

```js
emitter.removeAllListeners("join");
```

is case mey koee listener k name pass karney k zrorat nahi qn k jab sarey hi remove karney hey to specific pass krna sense nahi banata.

## How to make a listener to respond only once no matters if an an event is occurred mulitple times?

By default jab ham aik listener ko `emitter` class k `on()` method ko use kar k attach kartey heyn kisi bhi event k sath to jitni baat woh event in our case the `join` event occurred hoga woh listner bhi execute hoga.

## Why we inherit the Event Emitter class?

We often **inherit (extend)** the `EventEmitter` class because it allows our own **custom classes or objects** to gain the ability to **emit** and **listen for events**.

```js
const EventEmitter = require("node:events");

class ChatRoom extends EventEmitter {
  constructor() {
    super();
    this.users = new Set();
  }

  join(user) {
    if (this.users.has(user)) {
      console.log(`A user with name ${user} alread exists!`);
    } else {
      this.users.add(user);
      this.emit("join", user);
    }
  }

  sendMessage(user, message) {
    if (this.users.has(user)) {
      this.emit("message", user, message);
    } else {
      console.log("Please register yourself with us.");
    }
  }

  leave(user) {
    if (this.users.has(user)) {
      this.users.delete(user);
      this.emit("left", user);
    } else {
      console.log("This kind of operation is'nt allowd!");
    }
  }
}

module.exports = ChatRoom;
```

client side code:-

```js

```
