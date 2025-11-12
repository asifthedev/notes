## Stack Memory

- **Primitive Data Types:**
  
  The Stack is used for storing primitive data types, which include `number`, `string`, `boolean`, `null`, `undefined`, and `symbol`. When a variable is assigned a primitive value, a direct copy of that value is stored on the Stack.

- **Function Calls:**
  
  The Call Stack, a specific type of stack, is used to manage function execution. Each time a function is called, a new "frame" or "execution context" is pushed onto the Call Stack. This frame contains information like the function's local variables and the point to return to after the function completes.

- **LIFO Structure:**
  
  The Stack operates on a Last-In, First-Out (LIFO) principle, similar to a stack of plates. Items are added and removed from the top, making memory allocation and deallocation very fast and efficient.

- **Automatic Management:**
  
  Memory on the Stack is automatically managed. When a function finishes executing, its corresponding frame is popped off the Call Stack, and the memory it occupied is automatically deallocated.

## Heap Memory

- **Non-Primitive Data Types:**
  
  The Heap is used for storing non-primitive data types, which include `objects`, `arrays`, and `functions`. These data types can be dynamic in size and require more flexible memory management.

- **References:**
  
  When a variable is assigned a non-primitive value, the actual data (the object or array) is stored on the Heap, and a reference (memory address) to that data is stored on the Stack. This means multiple variables can point to the same object in the Heap.

- **Dynamic Allocation:**
  
  Memory on the Heap is dynamically allocated as needed, allowing for flexible data structures that can grow or shrink during runtime.

- **Garbage Collection:**
  
  Unlike the Stack, Heap memory is not automatically deallocated when a function finishes. Instead, JavaScript uses a process called "Garbage Collection" to identify and reclaim memory that is no longer being referenced by any active part of the program. This prevents memory leaks.

In summary, the Stack handles static, fixed-size data and function execution flow, offering fast and automatic memory management. The Heap manages dynamic, variable-sized data, requiring references and relying on garbage collection for memory reclamation.
