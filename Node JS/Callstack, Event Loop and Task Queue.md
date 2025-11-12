## Callstack

JavaScript aik a single-threaded language hey, jab bhi code excecute hota hey to is aik execution thread k uper JS Engine aik execution callstack banata.

Is mey jo bhi code ata woh esa code hota hey jo immediately execute hona hota hey. Ager kuxh asynchronous hey to woh browser API ko dey diya jata hey.

Jab woh asynchronous task complete ho jata hey to browser api usay uski type k hisab say ya to **macros task queue** ya phir microtask queue mey daal deyti hey ya phir microtask queue mey.

Abh in dono mey say kisi bhi queue say koee completed task tabhi callstack mey execustion kelye bheja jaye ga jab callstack empty hoga, is cheez ko check karney kelye aik loop constantly run karti rehti hey jo k event loop kahlati hey. Iska kaam hey k jesay hi callstack free ho yeah task queue say task main execution callstack mey execution kelye dal dey.

## **Macro Task Queue**

ismey macro task jesay file read karna aur I/O bound task and `setTimeOut()`, `setInterVal()`or DOM k events wagaira run hotey heyn.

## Micro Task Queue

yeah high priority queue hoti hey is queue mey majud task ko macro task mey majud task say pehlay execute kia jata hey. ismey high priority micro task run hotey jesay k promises k then(), catch, finally wagaira, 

## Starvation

Ager micro task mey majud task kabhi khatam hi na ho jis ki wajah say macro task mey majud tasks ko execute honey ka time hi nahi milta, isay starvation kehtay heyn


