# Resources

1. # Event

The event loop is what allows Node.js to perform non-blocking I/O operations by offloading operations to the system kernel whenever possible.

Ye **JavaScript engine** aur **libuv** ke darmiyan **coordination layer** ka kaam karta hai.

Jab bhi koi **asynchronous task** (jaise file read, network request, timer, etc.) aata hai:

1. Node.js us task ko **main JS thread se offload** karta hai.

2. Us task ko **Node.js bindings** ke zariye **libuv** ko diya jata hai.

3. **libuv** is task ko **worker thread pool** me execute karta hai.

4. Jab execution complete hoti hai, result ke sath **callback function** ko **uske related queue** (jaise timer queue, I/O queue, etc.) me daal diya jata hai.

5. **Event loop** continuously check karta hai — agar **main thread free** hai to ye **queue se callbacks** pick karke execute karwata hai.

### **Browser aur Node.js me Asynchronous Execution ka Comparison**

**Browser me:**  
Jab koi asynchronous task (jaise `setTimeout`, `fetch`, `DOM event`, etc.) milta hai,  
to JavaScript engine usay **Web APIs** ko de deta hai.  
Web APIs background me kaam karti rehti hain — jaise hi task complete hota hai,  
uska **callback** ya **promise** result **callback queue** ya **microtask queue** me daal diya jata hai.  
Phir **event loop** in queues ko check karke callbacks execute karta hai jab **main thread free** hota hai.

**Node.js me:**  
Bilkul isi tarah, jab koi asynchronous task (jaise file read, database query, ya timer) milta hai,  
to Node.js usay **libuv library** ko **offload** kar deta hai.  
`libuv` ke paas **thread pool** hota hai jo ye tasks background me execute karta hai —  
isse **main JS thread** free rehta hai aur **non-blocking I/O** possible hoti hai.  
Jab task complete ho jata hai, uska **callback** **relevant queue** (jaise I/O queue, timer queue, etc.) me daal diya jata hai.  
Phir **event loop** in queues se callbacks pick karke **main thread** par execute karta hai.

## How Event Loop works in node?

According to node JS documentation event loop k ander different types k asyncronous oeprations kelye **6 different** task queues hoti heyn jinko one by one execute kia jata hey.

```js
   ┌───────────────────────────┐
┌─>│           timers          │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │     pending callbacks     │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
│  │       idle, prepare       │
│  └─────────────┬─────────────┘      ┌───────────────┐
│  ┌─────────────┴─────────────┐      │   incoming:   │
│  │           poll            │<─────┤  connections, │
│  └─────────────┬─────────────┘      │   data, etc.  │
│  ┌─────────────┴─────────────┐      └───────────────┘
│  │           check           │
│  └─────────────┬─────────────┘
│  ┌─────────────┴─────────────┐
└──┤      close callbacks      │
   └───────────────────────────┘
```

### Timer Phase

Yaha pay timer function `setTimeOut()` or `setInteral()` exectue hotay heyn.

## Pending Callbacks

This phase executes callbacks for some system operations such as types of TCP errors. For example if a TCP socket receives `ECONNREFUSED` when attempting to connect, some *nix systems want to wait to report the error.

## Poll Phase

This is the most important phase in the cycle of event loop. All I/O task such as Network Request, File Reading, wagaira k callbacks ko isi phase ki queue mey line-up kiya jata hey.

https://youtu.be/os7KcmJvtN4?si=XPn62ZboVJaciCJh

[NODE JS Official Doc.](https://nodejs.org/en/learn/asynchronous-work/event-loop-timers-and-nexttick)

[How NodeJS Works? (Piush Garg)](https://youtu.be/_eJ6KAb56Gw?si=LUAihfm_6Kt2wnBO
