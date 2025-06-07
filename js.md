#### 1. What is the difference between == and === in JavaScript?
== compares values with type coercion.

=== compares values without coercion, checking both value and type.

```bash
0 == '0'; // true
0 === '0'; // false
```

#### 2. What is the Temporal Dead Zone (TDZ)?
The TDZ is the period between entering the scope and the actual declaration of let or const variables.

```bash
console.log(x); // ReferenceError
let x = 10;
```

#### 3. What is event delegation?
It’s a technique of using a single event listener on a parent element to handle events from its child elements.

```bash
document.getElementById('parent').addEventListener('click', function(e) {
  if (e.target.matches('.child')) {
    console.log('Child clicked');
  }
});
```

#### 4. Explain the concept of closures.
A closure gives you access to an outer function’s scope from an inner function.

```bash
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  }
}
const counter = outer();
counter(); // 1
counter(); // 2
```

#### 5. Difference between var, let, and const?
var: function-scoped, hoisted, can be redeclared.

let: block-scoped, not hoisted to usable state (TDZ), can be updated but not redeclared.

const: block-scoped, cannot be updated or redeclared.


#### 6. What does typeof null return and why?
Returns "object" due to a bug in the initial implementation of JavaScript.

#### 7. How does JavaScript handle asynchronous code?
With event loop, callback queue, and microtask queue (Promises are in microtask queue).

#### 8. Difference between synchronous and asynchronous code?
Synchronous: blocks execution.

Asynchronous: non-blocking, deferred execution.

#### 9. Explain the event loop in JavaScript.
JavaScript uses a single-threaded event loop model to handle concurrency via queues (macrotasks and microtasks).

#### 10. What is a Promise and its states?
A Promise represents a value that may be available in the future.

States:

Pending

Fulfilled

Rejected

#### 11. What is hoisting?
Variable and function declarations are moved to the top of their scope before code execution.

```bash
console.log(x); // undefined
var x = 5;
```

#### 12. What are arrow functions and their differences from regular functions?
Arrow functions:

Don’t have their own this

Can’t be used as constructors

Can’t use arguments

```bash
const fn = () => console.log(this); // this is lexically scoped
```

#### 13. What are IIFEs?
Immediately Invoked Function Expressions, used to create a private scope.

```bash
(function() {
  // private scope
})();
```

#### 14. What is the difference between call, apply, and bind?
call: invokes with this and arguments

apply: same as call, but arguments as array

bind: returns a new function with bound this

#### 15. What is memoization?
An optimization technique to cache function results.

```bash
function memo(fn) {
  const cache = {};
  return function(n) {
    if (cache[n]) return cache[n];
    cache[n] = fn(n);
    return cache[n];
  };
}
```

#### 16. What is the difference between setTimeout and setInterval?
setTimeout: runs once after delay

setInterval: runs repeatedly after interval

#### 17. Explain debounce vs throttle.
Debounce: delay execution until after a pause.

Throttle: limits execution to once every set time.

#### 18. What is currying?
Transforming a function with multiple arguments into a sequence of unary functions.

```bash
function curry(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}
```

#### 19. What are higher-order functions?
Functions that take other functions as arguments or return them.

#### 20. Explain prototype-based inheritance.
JavaScript uses prototypes to inherit properties/methods.

```bash
function Person(name) {
  this.name = name;
}
Person.prototype.sayHello = function() {
  console.log(`Hello, ${this.name}`);
};
```

#### 21. What is Object.create used for?
To create a new object with a specified prototype.

```bash
const parent = { greet: () => "hi" };
const child = Object.create(parent);
```

#### 22. Explain the difference between .map(), .filter(), and .reduce().
map: transforms

filter: filters

reduce: accumulates

#### 23. What is the difference between == and Object.is?
Object.is is more strict than === for special cases like NaN and -0.

```bash
NaN === NaN; // false
Object.is(NaN, NaN); // true
```

#### 24. What is destructuring?
Unpacking values from arrays/objects.

```bash
const [a, b] = [1, 2];
const {x, y} = {x: 10, y: 20};
```

#### 25. What is a generator function?
Used to create iterators using function* and yield.

```bash
function* gen() {
  yield 1;
  yield 2;
}
```

#### 26. Difference between shallow and deep copy?
Shallow copy copies references.

Deep copy duplicates nested objects.

```bash
const deep = JSON.parse(JSON.stringify(obj));
```

#### 27. What is the difference between null and undefined?
undefined: uninitialized

null: explicitly empty

#### 28. What are symbols in JS?
Unique and immutable identifiers.

```bash
const sym = Symbol('id');
```

#### 29. How does this work in different contexts?
Global: window (non-strict), undefined (strict)

Object: object

Arrow: lexical

#### 30. Can you polyfill bind?
Yes:

```bash
Function.prototype.myBind = function(context, ...args) {
  return (...rest) => this.apply(context, [...args, ...rest]);
};
```

#### 31. Explain optional chaining (?.).
Safely access deeply nested properties.

```bash
user?.address?.street
```

#### 32. What is the difference between for...in and for...of?
for...in: keys of object

for...of: values of iterable

#### 33. What is Object.freeze()?
Freezes object — no additions, deletions, or updates.

#### 34. What is the difference between Array.forEach and Array.map?
forEach: side-effects

map: returns a new array

#### 35. What is tail call optimization?
Optimization where last function call returns directly without growing stack.

#### 36. Explain async/await under the hood.
It’s syntactic sugar over Promises and generators.

#### 37. What is a WeakMap?
Map-like collection where keys are weakly referenced objects.

#### 38. Can you reassign const objects?
You can mutate their properties but not reassign them.

#### 39. Difference between == and === for objects?
Always false unless referencing same object.

#### 40. What is the output of [1, 2, 3] + [4, 5, 6]?
String: '1,2,34,5,6'

#### 41. What is NaN and how to check it properly?
Represents "Not a Number".

Use Number.isNaN().

#### 42. Can you override built-in prototypes?
Yes, but not recommended.

```bash
Array.prototype.myFunc = () => {};
```

#### 43. Explain JavaScript memory leaks.
Caused by:

Detached DOM nodes

Closures holding references

Forgotten timers or intervals

#### 44. What is the use of Object.entries() and Object.fromEntries()?
Convert objects to/from arrays of key-value pairs.

#### 45. What is the output of typeof NaN?
"number" — because NaN is a numeric value.

#### 46. Explain call stack and task queue.
Call stack: where functions are executed.

Task queue: where async callbacks wait.

#### 47. What is a polyfill?
Code that provides fallback implementation of newer features.

#### 48. What is a transpiler like Babel?
Converts ES6+ code to compatible ES5 code.

#### 49. How does garbage collection work in JS?
JS uses reference-counting and mark-and-sweep algorithms.

#### 50. How do you handle race conditions in async JS?
Use Promise.all, Promise.race

AbortControllers

Mutex/semaphores