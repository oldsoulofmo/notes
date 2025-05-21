###  An high-level overview of javascript

Javascript is a high level, prototype-based, object-oriented, multi-paradigm, interpreted or just-in-time compiled, dynamic, single-threaded and garbage-collected programming language with first class functions and non-blocking event loop concurrency model.

High-level means that developers do not need to worry about managing resources, in the other hand we have low-level programming languages as C where developers need to manage resources.

Garbage-collector is an already defined algorithm in JavaScript that cleans the computer's memory from any unused objects.

A paradigm is an approach and mindset of structuring code.
- Procedural programming.
- OOP.
- FP. 

		JavaScript accepts all of these paradigms.

First-class functions, means that functions are simply treated as variables, we can pass them into other functions and return them from other functions.

Dynamically-typed, we do not define the type of variables and it only becomes known when the engine executes our code, also data types are changed by reassigning the variables to another type of value. 

	Concurrency-model is how the JavaScript engine handles multiple tasks happening at the same time.
	
	JavaScript runs in one single thread, so it can only do one thing at a time.

	A thread is a set of instructions executed in the CPU, the thread is where the code is executed in machine's processor.

	If we have a long task, we do not want it to block the single thread to execute the upcomming task.

	By using an event loop we take long running tasks and execute them in the background then put them back in the main thread once they're finished.

### The JavaScript engine and runtime 

Just in time compilation (JIT), the source code is converted into machine code at once then executed immediately.

An engine is a program that executes JavaScript code.

### Primitives vs Objects 

**Primitives** are referred to as _primitive_ types and **Objects** are referred to as _reference types_.
This is because Objects are stored in heap with a reference value, pointed at from the call stack as it is shown below : 

![[Screenshot 2023-07-10 at 17.04.32.png]]

This has so many downfalls as for copying objects and then changing it's properties will affect the main object from the root : 

```javascript
const me = {
	name : mohammed,
	age : 22
}
const friend = me;
friend.age = 25;
```

![[Screenshot 2023-07-10 at 17.11.39 1.png]]

As we see in here, the object `me` has changed from the ground up ! 

	Only primitives created with const cannot be changed ever, reference types can be changed as seen in the example above, but the adress do not change !

