# Node.js Interview Questions and Answers

> Based on [roadmap.sh/nodejs](https://roadmap.sh/nodejs) - Comprehensive Interview Preparation Guide

---

## Table of Contents

1. [Node.js Fundamentals](#nodejs-fundamentals)
2. [JavaScript Basics for Node.js](#javascript-basics-for-nodejs)
3. [Variables and Constants](#variables-and-constants)
4. [Modules and Package Management](#modules-and-package-management)
5. [Asynchronous Programming](#asynchronous-programming)
6. [Event Loop and Event-Driven Architecture](#event-loop-and-event-driven-architecture)
7. [Streams and Buffers](#streams-and-buffers)
8. [File System Operations](#file-system-operations)
9. [HTTP and Web Servers](#http-and-web-servers)
10. [Express.js Framework](#expressjs-framework)
11. [Middleware](#middleware)
12. [RESTful APIs](#restful-apis)
13. [Database Connections](#database-connections)
14. [ORM and Query Builders](#orm-and-query-builders)
15. [Database Migrations](#database-migrations)
16. [CRUD Operations](#crud-operations)
17. [Message Brokers](#message-brokers)
18. [Caching with Redis](#caching-with-redis)
19. [Authentication](#authentication)
20. [Authorization](#authorization)
21. [Security Practices](#security-practices)
22. [Error Handling](#error-handling)
23. [Testing](#testing)
24. [Server-Side Rendering](#server-side-rendering)
25. [Performance Optimization](#performance-optimization)
26. [Deployment and DevOps](#deployment-and-devops)
27. [Advanced Topics](#advanced-topics)

---


## Node.js Fundamentals

### Q1. What is Node.js? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Backend, Basics, Web

**Answer:**

Node.js is an open-source, cross-platform JavaScript runtime environment built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript code on the server-side, outside of web browsers.

**Key Characteristics:**

1. **Runtime Environment:** Not a programming language or framework, but a runtime that executes JavaScript
2. **V8 Engine:** Uses Google's V8 engine to compile JavaScript to native machine code
3. **Event-Driven:** Built on an event-driven, non-blocking I/O model
4. **Single-Threaded:** Uses a single-threaded event loop (with worker threads for CPU-intensive tasks)
5. **NPM:** Comes with npm (Node Package Manager), the world's largest software registry

**Use Cases:**
- Backend API development
- Real-time applications (chat, gaming)
- Microservices architecture
- Server-side rendering
- Command-line tools
- IoT applications
- Streaming applications

**Example:**
```javascript
// Simple HTTP server
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, Node.js!');
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

---

## Node.js Fundamentals

### Q1. What is Node.js? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Backend, Basics, Web

**Answer:**

Node.js is an open-source, cross-platform JavaScript runtime environment built on Chrome's V8 JavaScript engine. It allows developers to run JavaScript code on the server-side, outside of web browsers.

**Key Characteristics:**

1. **Runtime Environment:** Not a programming language or framework, but a runtime that executes JavaScript
2. **V8 Engine:** Uses Google's V8 engine to compile JavaScript to native machine code
3. **Event-Driven:** Built on an event-driven, non-blocking I/O model
4. **Single-Threaded:** Uses a single-threaded event loop (with worker threads for CPU-intensive tasks)
5. **NPM:** Comes with npm (Node Package Manager), the world's largest software registry

**Architecture:**

```
┌─────────────────┐
│   JavaScript    │
│     Code        │
└────────┬────────┘
         │
┌────────▼────────┐
│  Node.js APIs   │
│  (fs, http, etc)│
└────────┬────────┘
         │
┌────────▼────────┐
│   V8 Engine     │
│  (JavaScript    │
│   Compiler)     │
└────────┬────────┘
         │
┌────────▼────────┐
│  Operating      │
│  System         │
└─────────────────┘
```

**Use Cases:**
- Backend API development
- Real-time applications (chat, gaming)
- Microservices architecture
- Server-side rendering
- Command-line tools
- IoT applications
- Streaming applications

**Example:**
```javascript
// Simple HTTP server
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, Node.js!');
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

**Advantages:**
- Fast execution (V8 engine)
- Large ecosystem (npm packages)
- JavaScript everywhere (same language for frontend and backend)
- Non-blocking I/O (handles many concurrent connections)
- Active community

**Disadvantages:**
- Not suitable for CPU-intensive tasks (can use worker threads)
- Callback hell (mitigated by Promises/async-await)
- Immature in some areas compared to established languages

---

### Q2. How does Node.js differ from traditional server-side technologies? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Architecture, Web

**Answer:**

Node.js differs significantly from traditional server-side technologies like PHP, Java, or Python in several key ways:

**1. Threading Model:**

**Traditional (Multi-threaded):**
```java
// Java example - each request gets a thread
Thread thread = new Thread(() -> {
    // Handle request
});
thread.start();
```
- Each request spawns a new thread
- Threads consume memory (typically 1-2MB per thread)
- Limited scalability (thread pool exhaustion)
- Context switching overhead

**Node.js (Single-threaded with Event Loop):**
```javascript
// Node.js - single thread handles all requests
server.on('request', (req, res) => {
  // Non-blocking operations
  fs.readFile('file.txt', (err, data) => {
    res.end(data);
  });
});
```
- Single main thread handles all requests
- Non-blocking I/O operations
- Event loop manages concurrency
- Can handle thousands of concurrent connections

**2. Programming Language:**

| Traditional | Node.js |
|------------|---------|
| PHP, Java, Python, Ruby | JavaScript |
| Different language for frontend/backend | Same language (JavaScript) |
| Need to learn multiple languages | Unified language |

**3. I/O Model:**

**Traditional (Blocking I/O):**
```python
# Python - blocking I/O
data = file.read()  # Blocks until complete
process(data)        # Executes after file read
```

**Node.js (Non-blocking I/O):**
```javascript
// Node.js - non-blocking I/O
fs.readFile('file.txt', (err, data) => {
  // Callback executes when file is read
  process(data);
});
// Code continues immediately
```

**4. Performance Comparison:**

| Metric | Traditional | Node.js |
|--------|------------|---------|
| Concurrent Connections | Limited by threads | Thousands |
| Memory Usage | High (per thread) | Low (shared event loop) |
| I/O Performance | Blocking | Non-blocking |
| CPU-intensive Tasks | Good | Not ideal (use worker threads) |

**When to Use Node.js:**
- Real-time applications
- High I/O operations
- Microservices
- API servers
- Data streaming

**When NOT to Use Node.js:**
- CPU-intensive computations (image processing, video encoding)
- Heavy mathematical calculations
- Applications requiring strict type safety

---


### Q3. What is the Node.js event loop? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Asynchronous, Event Loop, I/O Operations

**Answer:**

The event loop is the core mechanism that allows Node.js to perform non-blocking I/O operations despite JavaScript being single-threaded. It's responsible for executing code, collecting and processing events, and executing queued sub-tasks.

**Event Loop Phases:**

The event loop operates in several phases, each with its own callback queue:

1. **Timers Phase:** Executes callbacks scheduled by `setTimeout()` and `setInterval()`
2. **Pending Callbacks Phase:** Executes I/O callbacks deferred to the next loop iteration
3. **Idle, Prepare Phase:** Internal use only, prepares for the next phase
4. **Poll Phase:** Fetches new I/O events and executes I/O-related callbacks
5. **Check Phase:** Executes `setImmediate()` callbacks
6. **Close Callbacks Phase:** Executes close callbacks (e.g., `socket.on('close')`)

**Priority Order:**

```
process.nextTick() > setImmediate() > setTimeout() > I/O callbacks
```

**Example:**
```javascript
console.log('1. Start');

setTimeout(() => console.log('2. setTimeout'), 0);
setImmediate(() => console.log('3. setImmediate'));
process.nextTick(() => console.log('4. nextTick'));

console.log('5. End');

// Output:
// 1. Start
// 5. End
// 4. nextTick
// 2. setTimeout
// 3. setImmediate
```

**Key Points:**
- Single-threaded (main thread)
- Non-blocking I/O operations
- Callbacks are queued and executed
- Never blocks (except when polling phase is empty and no timers)
- Efficient for I/O-bound applications

---

### Q4. What is the difference between process.nextTick() and setImmediate()? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Asynchronous, Event Loop

**Answer:**

Both `process.nextTick()` and `setImmediate()` are used to schedule callbacks, but they have different priorities and execution timings in the event loop.

**process.nextTick():**
- **Priority:** Highest priority (executes before any other phase)
- **Queue:** Has its own microtask queue
- **Execution:** Executes immediately after the current operation completes
- **Use Case:** Ensure a callback runs before any other async operation

**setImmediate():**
- **Priority:** Lower than `process.nextTick()`, but executes in the Check phase
- **Queue:** Part of the event loop's Check phase
- **Execution:** Executes after the Poll phase completes
- **Use Case:** Execute callbacks after I/O events in the current event loop cycle

**Execution Order Example:**
```javascript
console.log('1. Start');

setTimeout(() => console.log('2. setTimeout'), 0);
setImmediate(() => console.log('3. setImmediate'));
process.nextTick(() => console.log('4. nextTick'));

Promise.resolve().then(() => console.log('5. Promise'));

console.log('6. End');

// Output:
// 1. Start
// 6. End
// 4. nextTick        ← Highest priority
// 5. Promise         ← Microtask queue
// 2. setTimeout      ← Timers phase
// 3. setImmediate    ← Check phase
```

**Key Differences:**

| Feature | process.nextTick() | setImmediate() |
|---------|-------------------|----------------|
| Priority | Highest | Lower |
| Phase | Microtask queue | Check phase |
| Execution | Before event loop continues | After Poll phase |
| Recursion | Can starve event loop | Safer for recursion |

---

### Q5. What is the package.json file and what are its key properties? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Package Management, Project Management

**Answer:**

`package.json` is a manifest file that contains metadata about a Node.js project. It's the central configuration file for npm (Node Package Manager) and defines project dependencies, scripts, and other project information.

**Key Properties:**

**1. Basic Information:**
```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My awesome Node.js application",
  "main": "index.js",
  "author": "John Doe",
  "license": "MIT"
}
```

**2. Dependencies:**
```json
{
  "dependencies": {
    "express": "^4.18.0",
    "mongoose": "^6.0.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.0",
    "jest": "^28.0.0"
  }
}
```

**3. Scripts:**
```json
{
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  }
}
```

**Version Ranges:**
- `^4.18.0` - Compatible with 4.18.0 to <5.0.0
- `~4.17.21` - Compatible with 4.17.21 to <4.18.0
- `1.2.0` - Exact version
- `>=2.0.0` - Minimum version

---

## JavaScript Basics for Node.js

### Q6. What are the different ways to declare variables in JavaScript? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Constants, JavaScript Basics

**Answer:**

JavaScript provides three ways to declare variables: `var`, `let`, and `const`.

**1. var (Function-scoped):**
```javascript
var name = "John";
var age = 30;

function example() {
  var localVar = "I'm function-scoped";
  if (true) {
    var blockVar = "I'm also function-scoped";
  }
  console.log(blockVar); // Works! (not block-scoped)
}
```

**Characteristics:**
- Function-scoped (not block-scoped)
- Can be redeclared
- Hoisted (declaration moved to top)
- Can be used before declaration (undefined)

**2. let (Block-scoped):**
```javascript
let name = "John";
let age = 30;

function example() {
  let localVar = "I'm block-scoped";
  if (true) {
    let blockVar = "I'm block-scoped";
    console.log(blockVar); // Works
  }
  // console.log(blockVar); // Error! Not accessible
}
```

**Characteristics:**
- Block-scoped
- Cannot be redeclared in same scope
- Hoisted but in "temporal dead zone"
- Cannot be used before declaration

**3. const (Block-scoped, Immutable):**
```javascript
const PI = 3.14159;
const user = { name: "John", age: 30 };

// PI = 3.14; // Error! Cannot reassign
user.age = 31; // OK! Object properties can change
```

**Characteristics:**
- Block-scoped
- Must be initialized
- Cannot be reassigned
- Object/array contents can be modified (reference is constant)

**Comparison:**

| Feature | var | let | const |
|---------|-----|-----|-------|
| Scope | Function | Block | Block |
| Redeclare | Yes | No | No |
| Reassign | Yes | Yes | No |
| Hoisting | Yes (undefined) | Yes (TDZ) | Yes (TDZ) |
| Initialization | Optional | Optional | Required |

**Best Practices:**
- Use `const` by default
- Use `let` when reassignment is needed
- Avoid `var` (legacy, use only if necessary)

---

### Q7. What is the difference between == and === in JavaScript? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Operators, JavaScript Basics

**Answer:**

`==` (loose equality) and `===` (strict equality) are comparison operators with different behaviors.

**== (Loose Equality):**
- Performs type coercion before comparison
- Converts operands to same type if needed
- Can lead to unexpected results

**=== (Strict Equality):**
- No type coercion
- Compares both value and type
- More predictable and recommended

**Examples:**
```javascript
// Loose equality (==)
5 == "5"        // true (type coercion)
0 == false      // true (type coercion)
null == undefined // true (special case)
"" == false     // true (type coercion)

// Strict equality (===)
5 === "5"       // false (different types)
0 === false     // false (different types)
null === undefined // false (different types)
"" === false    // false (different types)

// Object comparison
{} == {}        // false (different references)
{} === {}       // false (different references)
```

**Type Coercion Rules (==):**
```javascript
// String to Number
"5" == 5        // true

// Boolean to Number
true == 1       // true
false == 0      // true

// null and undefined
null == undefined // true
null == 0       // false
undefined == 0  // false

// Special cases
NaN == NaN      // false (NaN is never equal to itself)
```

**Best Practice:**
Always use `===` (strict equality) unless you specifically need type coercion.

```javascript
// Good
if (age === 18) { }
if (name === "John") { }

// Avoid
if (age == 18) { }
if (name == "John") { }
```

---

### Q8. What are arrow functions in JavaScript? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Functions, JavaScript Basics

**Answer:**

Arrow functions are a concise syntax for writing functions in JavaScript, introduced in ES6. They provide a shorter syntax and lexically bind `this`.

**Syntax:**
```javascript
// Traditional function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => {
  return a + b;
};

// Implicit return (single expression)
const add = (a, b) => a + b;

// Single parameter (no parentheses needed)
const square = x => x * x;

// No parameters
const greet = () => console.log("Hello");

// Multiple statements
const process = (data) => {
  const result = data.map(x => x * 2);
  return result.filter(x => x > 10);
};
```

**Key Differences:**

**1. `this` Binding:**
```javascript
// Traditional function - `this` is dynamic
const obj = {
  name: "John",
  greet: function() {
    console.log(this.name); // "John"
    setTimeout(function() {
      console.log(this.name); // undefined (this is window/global)
    }, 1000);
  }
};

// Arrow function - `this` is lexical
const obj = {
  name: "John",
  greet: function() {
    console.log(this.name); // "John"
    setTimeout(() => {
      console.log(this.name); // "John" (this is bound to obj)
    }, 1000);
  }
};
```

**2. Arguments Object:**
```javascript
// Traditional function
function example() {
  console.log(arguments); // Arguments object
}

// Arrow function - no arguments object
const example = () => {
  // console.log(arguments); // Error!
  // Use rest parameters instead
};

const example = (...args) => {
  console.log(args); // Array
};
```

**3. Cannot be used as constructors:**
```javascript
// Traditional function
function Person(name) {
  this.name = name;
}
const person = new Person("John"); // OK

// Arrow function
const Person = (name) => {
  this.name = name;
};
// const person = new Person("John"); // Error!
```

**When to Use Arrow Functions:**
- Callbacks and array methods
- When you need lexical `this`
- Short, simple functions

**When NOT to Use:**
- Object methods (if you need `this` to be the object)
- Constructors
- Functions that need `arguments` object
- Event handlers (sometimes)

---

## Variables and Constants

### Q9. What is the difference between let, const, and var? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Constants, Scope, Hoisting

**Answer:**

This is a fundamental question about variable declarations in JavaScript. Let's explore the differences in detail.

**1. Scope:**

**var - Function Scope:**
```javascript
function example() {
  if (true) {
    var x = 10;
  }
  console.log(x); // 10 (accessible outside block)
}

for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 3, 3, 3
}
```

**let/const - Block Scope:**
```javascript
function example() {
  if (true) {
    let x = 10;
    const y = 20;
  }
  // console.log(x); // Error! Not accessible
  // console.log(y); // Error! Not accessible
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 0, 1, 2
}
```

**2. Hoisting:**

**var:**
```javascript
console.log(x); // undefined (not error)
var x = 5;

// Equivalent to:
var x;
console.log(x); // undefined
x = 5;
```

**let/const:**
```javascript
// console.log(x); // Error! Cannot access before initialization
let x = 5;

// Temporal Dead Zone (TDZ)
// x exists but cannot be accessed until declaration
```

**3. Redeclaration:**

```javascript
var x = 1;
var x = 2; // OK

let y = 1;
// let y = 2; // Error! Cannot redeclare

const z = 1;
// const z = 2; // Error! Cannot redeclare
```

**4. Reassignment:**

```javascript
var x = 1;
x = 2; // OK

let y = 1;
y = 2; // OK

const z = 1;
// z = 2; // Error! Cannot reassign
```

**5. Initialization:**

```javascript
var x; // OK, undefined
let y; // OK, undefined
// const z; // Error! Must be initialized
```

**6. Loop Behavior:**

```javascript
// var in loop
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 3, 3, 3
}

// let in loop
for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 100); // 0, 1, 2
}
```

**Best Practices:**
1. Use `const` by default
2. Use `let` when you need to reassign
3. Avoid `var` (legacy, use only if necessary for compatibility)

---

### Q10. What is hoisting in JavaScript? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer  
**Tags:** Programming, Variables, Hoisting, JavaScript Basics

**Answer:**

Hoisting is a JavaScript mechanism where variable and function declarations are moved to the top of their containing scope during the compilation phase, before code execution.

**Variable Hoisting:**

**var:**
```javascript
console.log(x); // undefined (not error)
var x = 5;

// What actually happens:
var x;           // Declaration hoisted
console.log(x); // undefined
x = 5;          // Assignment stays in place
```

**let/const:**
```javascript
// console.log(x); // ReferenceError! Cannot access before initialization
let x = 5;

// Temporal Dead Zone (TDZ)
// Declaration is hoisted but variable is in TDZ until initialization
```

**Function Hoisting:**

**Function Declarations:**
```javascript
sayHello(); // "Hello!" (works!)

function sayHello() {
  console.log("Hello!");
}

// Entire function is hoisted
```

**Function Expressions:**
```javascript
// sayHello(); // TypeError! sayHello is not a function

var sayHello = function() {
  console.log("Hello!");
};

// Only declaration is hoisted, not the assignment
```

**Arrow Functions:**
```javascript
// sayHello(); // ReferenceError!

const sayHello = () => {
  console.log("Hello!");
};

// Behaves like let/const
```

**Class Hoisting:**
```javascript
// const obj = new MyClass(); // ReferenceError!

class MyClass {
  constructor() {
    console.log("Created");
  }
}

// Classes are hoisted but remain in TDZ
```

**Hoisting Order:**
```javascript
// 1. Function declarations (highest priority)
// 2. Variable declarations (var)
// 3. let/const (in TDZ)

console.log(typeof myFunc); // "function"
console.log(typeof myVar);  // "undefined"

function myFunc() {}
var myVar = 5;
```

**Practical Example:**
```javascript
var x = 1;

function example() {
  console.log(x); // undefined (not 1!)
  var x = 2;
  console.log(x); // 2
}

example();
```

**Best Practices:**
1. Declare variables at the top of their scope
2. Use `let`/`const` instead of `var`
3. Declare functions before using them
4. Use linters to catch hoisting issues

---


## Object-Oriented Programming (OOPs)

### Q11. How does Object-Oriented Programming work in JavaScript? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, OOPs, Classes, Objects, JavaScript Basics

**Answer:**

JavaScript supports Object-Oriented Programming through prototypes (prototype-based OOP) and ES6 classes (syntactic sugar over prototypes).

**1. Constructor Functions (Traditional):**
```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.greet = function() {
  return `Hello, I'm ${this.name}`;
};

const person = new Person("John", 30);
console.log(person.greet()); // "Hello, I'm John"
```

**2. ES6 Classes:**
```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    return `Hello, I'm ${this.name}`;
  }

  // Static method
  static createAdult(name) {
    return new Person(name, 18);
  }
}

const person = new Person("John", 30);
console.log(person.greet()); // "Hello, I'm John"
```

**3. Inheritance:**
```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} makes a sound`;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }

  speak() {
    return `${this.name} barks`;
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
console.log(dog.speak()); // "Buddy barks"
```

**4. Encapsulation (Private Fields - ES2022):**
```javascript
class BankAccount {
  #balance = 0; // Private field

  deposit(amount) {
    this.#balance += amount;
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();
account.deposit(100);
// console.log(account.#balance); // Error! Private field
console.log(account.getBalance()); // 100
```

**5. Polymorphism:**
```javascript
class Shape {
  area() {
    throw new Error("Method must be implemented");
  }
}

class Circle extends Shape {
  constructor(radius) {
    super();
    this.radius = radius;
  }

  area() {
    return Math.PI * this.radius ** 2;
  }
}

class Rectangle extends Shape {
  constructor(width, height) {
    super();
    this.width = width;
    this.height = height;
  }

  area() {
    return this.width * this.height;
  }
}

const shapes = [
  new Circle(5),
  new Rectangle(4, 6)
];

shapes.forEach(shape => console.log(shape.area()));
```

**Key Concepts:**
- **Prototypes:** JavaScript uses prototype-based inheritance
- **Classes:** ES6 classes are syntactic sugar over prototypes
- **Inheritance:** Achieved through `extends` keyword
- **Encapsulation:** Private fields with `#` prefix
- **Polymorphism:** Different classes can implement same interface

---

### Q12. What is the difference between class and prototype in JavaScript? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, OOPs, Classes, Prototypes, JavaScript Basics

**Answer:**

Classes in JavaScript are syntactic sugar over prototype-based inheritance. Understanding both is crucial.

**Prototype-Based:**
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return `Hello, I'm ${this.name}`;
};

const person = new Person("John");
console.log(person.greet()); // "Hello, I'm John"
```

**Class-Based (ES6):**
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, I'm ${this.name}`;
  }
}

const person = new Person("John");
console.log(person.greet()); // "Hello, I'm John"
```

**Under the Hood:**
```javascript
// Class is converted to:
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function() {
  return `Hello, I'm ${this.name}`;
};
```

**Key Differences:**

| Feature | Prototype | Class |
|---------|-----------|-------|
| Syntax | Function-based | Class keyword |
| Hoisting | Function hoisted | Not hoisted (TDZ) |
| Strict Mode | Optional | Always strict |
| Constructor | Function itself | constructor() method |

**Prototype Chain:**
```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }
}

const dog = new Dog("Buddy", "Golden");

// Prototype chain:
// dog -> Dog.prototype -> Animal.prototype -> Object.prototype -> null

console.log(dog instanceof Dog);    // true
console.log(dog instanceof Animal); // true
console.log(dog instanceof Object); // true
```

---

## Modules and Package Management

### Q13. What are CommonJS and ES6 modules? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Modules, Package Management, Backend

**Answer:**

Node.js supports two module systems: CommonJS (traditional) and ES6 modules (modern).

**CommonJS (require/module.exports):**
```javascript
// math.js
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = {
  add,
  subtract
};

// Or individually:
// exports.add = add;
// exports.subtract = subtract;

// app.js
const math = require('./math');
console.log(math.add(2, 3)); // 5
```

**ES6 Modules (import/export):**
```javascript
// math.js
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}

// Or default export:
// export default { add, subtract };

// app.js
import { add, subtract } from './math.js';
// Or: import math from './math.js';

console.log(add(2, 3)); // 5
```

**Key Differences:**

| Feature | CommonJS | ES6 Modules |
|---------|----------|-------------|
| Syntax | require/module.exports | import/export |
| Loading | Synchronous | Asynchronous |
| Hoisting | Runtime | Compile-time |
| Tree Shaking | No | Yes |
| Dynamic Imports | No | Yes (import()) |
| Top-level await | No | Yes |

**Using ES6 Modules in Node.js:**
```json
// package.json
{
  "type": "module"
}
```

**Dynamic Imports (ES6):**
```javascript
// CommonJS - synchronous
const math = require('./math');

// ES6 - dynamic import (async)
const math = await import('./math.js');
```

**Mixed Usage:**
```javascript
// ES6 module importing CommonJS
import express from 'express'; // Works if express supports ES6

// CommonJS importing ES6 (not directly supported)
// Use dynamic import() instead
```

---

### Q14. How do you create and use npm packages? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Package Management, npm, Backend

**Answer:**

Creating and publishing npm packages is essential for code reuse and sharing.

**1. Creating a Package:**
```bash
# Initialize package
npm init -y

# Install dependencies
npm install express

# Install dev dependencies
npm install --save-dev jest
```

**2. Package Structure:**
```
my-package/
├── package.json
├── index.js          # Main entry point
├── lib/              # Source files
│   ├── utils.js
│   └── helpers.js
├── tests/            # Test files
│   └── test.js
├── README.md
└── .gitignore
```

**3. package.json Configuration:**
```json
{
  "name": "my-package",
  "version": "1.0.0",
  "description": "My awesome package",
  "main": "index.js",
  "scripts": {
    "test": "jest",
    "start": "node index.js"
  },
  "keywords": ["nodejs", "utility"],
  "author": "John Doe",
  "license": "MIT",
  "dependencies": {
    "express": "^4.18.0"
  },
  "devDependencies": {
    "jest": "^28.0.0"
  }
}
```

**4. Publishing to npm:**
```bash
# Login to npm
npm login

# Publish
npm publish

# Publish with specific version
npm version patch  # 1.0.0 -> 1.0.1
npm version minor   # 1.0.0 -> 1.1.0
npm version major   # 1.0.0 -> 2.0.0
npm publish
```

**5. Using Local Packages:**
```bash
# Link local package
npm link

# Use linked package
npm link my-package
```

**6. Scoped Packages:**
```json
{
  "name": "@mycompany/my-package",
  "version": "1.0.0"
}
```

**Best Practices:**
- Use semantic versioning
- Write comprehensive README
- Include tests
- Use .npmignore
- Follow naming conventions

---

## Asynchronous Programming

### Q15. What are Promises in JavaScript? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Asynchronous, Promises, Backend, I/O Operations

**Answer:**

Promises represent the eventual completion (or failure) of an asynchronous operation and its resulting value. They provide a cleaner alternative to callbacks.

**Creating Promises:**
```javascript
const promise = new Promise((resolve, reject) => {
  // Async operation
  setTimeout(() => {
    const success = true;
    if (success) {
      resolve("Operation successful");
    } else {
      reject("Operation failed");
    }
  }, 1000);
});
```

**Using Promises:**
```javascript
promise
  .then(result => {
    console.log(result); // "Operation successful"
    return "Next step";
  })
  .then(result => {
    console.log(result); // "Next step"
  })
  .catch(error => {
    console.error(error); // "Operation failed"
  })
  .finally(() => {
    console.log("Always executed");
  });
```

**Promise States:**
- **Pending:** Initial state, neither fulfilled nor rejected
- **Fulfilled:** Operation completed successfully
- **Rejected:** Operation failed

**Promise Methods:**
```javascript
// Promise.all - Wait for all
Promise.all([promise1, promise2, promise3])
  .then(results => {
    // All resolved
  })
  .catch(error => {
    // First rejection
  });

// Promise.allSettled - Wait for all (including rejections)
Promise.allSettled([promise1, promise2])
  .then(results => {
    // All completed (success or failure)
  });

// Promise.race - First to complete
Promise.race([promise1, promise2])
  .then(result => {
    // First resolved or rejected
  });

// Promise.any - First to resolve
Promise.any([promise1, promise2])
  .then(result => {
    // First resolved
  });
```

**Real-World Example:**
```javascript
function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) {
        resolve({ id, name: "John" });
      } else {
        reject("Invalid ID");
      }
    }, 1000);
  });
}

fetchUser(1)
  .then(user => {
    console.log(user); // { id: 1, name: "John" }
    return fetchUser(user.id + 1);
  })
  .then(user => {
    console.log(user); // { id: 2, name: "John" }
  })
  .catch(error => {
    console.error(error);
  });
```

---

### Q16. What is async/await and how does it work? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Asynchronous, async/await, Promises, Backend

**Answer:**

`async/await` is syntactic sugar over Promises that makes asynchronous code look and behave like synchronous code.

**Basic Syntax:**
```javascript
// Promise-based
function fetchData() {
  return fetch('/api/data')
    .then(response => response.json())
    .then(data => {
      console.log(data);
      return data;
    })
    .catch(error => {
      console.error(error);
    });
}

// async/await
async function fetchData() {
  try {
    const response = await fetch('/api/data');
    const data = await response.json();
    console.log(data);
    return data;
  } catch (error) {
    console.error(error);
  }
}
```

**Key Points:**
- `async` functions always return a Promise
- `await` pauses execution until Promise resolves
- `await` can only be used inside `async` functions
- Errors are caught with try/catch

**Multiple Async Operations:**
```javascript
// Sequential (slower)
async function sequential() {
  const user = await fetchUser(1);
  const posts = await fetchPosts(user.id);
  return { user, posts };
}

// Parallel (faster)
async function parallel() {
  const [user, posts] = await Promise.all([
    fetchUser(1),
    fetchPosts(1)
  ]);
  return { user, posts };
}
```

**Error Handling:**
```javascript
async function example() {
  try {
    const result = await asyncOperation();
    return result;
  } catch (error) {
    console.error("Error:", error);
    throw error; // Re-throw if needed
  }
}
```

**Real-World Example:**
```javascript
async function getUserWithPosts(userId) {
  try {
    const user = await db.users.findById(userId);
    if (!user) {
      throw new Error("User not found");
    }
    
    const posts = await db.posts.findByUserId(userId);
    
    return {
      ...user,
      posts
    };
  } catch (error) {
    console.error("Failed to fetch user:", error);
    throw error;
  }
}
```

---

## File System Operations

### Q17. How do you perform file I/O operations in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, I/O Operations, File System, Backend

**Answer:**

Node.js provides the `fs` module for file system operations, with both synchronous and asynchronous methods.

**1. Reading Files:**
```javascript
const fs = require('fs');

// Asynchronous (non-blocking)
fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(data);
});

// Synchronous (blocking)
try {
  const data = fs.readFileSync('file.txt', 'utf8');
  console.log(data);
} catch (err) {
  console.error(err);
}

// Promises (fs.promises)
const fsPromises = require('fs').promises;

async function readFile() {
  try {
    const data = await fsPromises.readFile('file.txt', 'utf8');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
```

**2. Writing Files:**
```javascript
// Asynchronous
fs.writeFile('file.txt', 'Hello World', 'utf8', (err) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log('File written');
});

// Synchronous
fs.writeFileSync('file.txt', 'Hello World', 'utf8');

// Append
fs.appendFile('file.txt', '\nNew line', 'utf8', (err) => {
  if (err) console.error(err);
});
```

**3. File Operations:**
```javascript
// Check if file exists
fs.access('file.txt', fs.constants.F_OK, (err) => {
  console.log(err ? 'File does not exist' : 'File exists');
});

// Get file stats
fs.stat('file.txt', (err, stats) => {
  if (err) {
    console.error(err);
    return;
  }
  console.log(stats.isFile());     // true
  console.log(stats.isDirectory()); // false
  console.log(stats.size);          // File size
});

// Delete file
fs.unlink('file.txt', (err) => {
  if (err) console.error(err);
});

// Rename file
fs.rename('old.txt', 'new.txt', (err) => {
  if (err) console.error(err);
});
```

**4. Directory Operations:**
```javascript
// Create directory
fs.mkdir('newdir', (err) => {
  if (err) console.error(err);
});

// Read directory
fs.readdir('.', (err, files) => {
  if (err) {
    console.error(err);
    return;
  }
  files.forEach(file => {
    console.log(file);
  });
});

// Remove directory
fs.rmdir('dir', (err) => {
  if (err) console.error(err);
});
```

**Best Practices:**
- Use asynchronous methods for non-blocking I/O
- Always handle errors
- Use `fs.promises` for Promise-based API
- Use streams for large files

---

### Q18. How do you perform CRUD operations using static JSON files? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, CRUD Operations, I/O Operations, File System

**Answer:**

Using static JSON files as a database is useful for simple applications, prototyping, or when a full database isn't needed.

**Setup:**
```javascript
const fs = require('fs').promises;
const path = require('path');

const DATA_FILE = path.join(__dirname, 'data.json');

// Initialize data file if it doesn't exist
async function initDataFile() {
  try {
    await fs.access(DATA_FILE);
  } catch {
    await fs.writeFile(DATA_FILE, JSON.stringify([], null, 2));
  }
}
```

**Read All (GET):**
```javascript
async function getAll() {
  try {
    const data = await fs.readFile(DATA_FILE, 'utf8');
    return JSON.parse(data);
  } catch (error) {
    console.error('Error reading file:', error);
    return [];
  }
}
```

**Read One (GET by ID):**
```javascript
async function getById(id) {
  try {
    const items = await getAll();
    return items.find(item => item.id === id);
  } catch (error) {
    console.error('Error getting item:', error);
    return null;
  }
}
```

**Create (POST):**
```javascript
async function create(newItem) {
  try {
    const items = await getAll();
    const id = items.length > 0 
      ? Math.max(...items.map(item => item.id)) + 1 
      : 1;
    
    const item = { id, ...newItem, createdAt: new Date().toISOString() };
    items.push(item);
    
    await fs.writeFile(DATA_FILE, JSON.stringify(items, null, 2));
    return item;
  } catch (error) {
    console.error('Error creating item:', error);
    throw error;
  }
}
```

**Update (PUT/PATCH):**
```javascript
async function update(id, updates) {
  try {
    const items = await getAll();
    const index = items.findIndex(item => item.id === id);
    
    if (index === -1) {
      throw new Error('Item not found');
    }
    
    items[index] = {
      ...items[index],
      ...updates,
      updatedAt: new Date().toISOString()
    };
    
    await fs.writeFile(DATA_FILE, JSON.stringify(items, null, 2));
    return items[index];
  } catch (error) {
    console.error('Error updating item:', error);
    throw error;
  }
}
```

**Delete (DELETE):**
```javascript
async function remove(id) {
  try {
    const items = await getAll();
    const filtered = items.filter(item => item.id !== id);
    
    if (items.length === filtered.length) {
      throw new Error('Item not found');
    }
    
    await fs.writeFile(DATA_FILE, JSON.stringify(filtered, null, 2));
    return true;
  } catch (error) {
    console.error('Error deleting item:', error);
    throw error;
  }
}
```

**Complete Example with Express:**
```javascript
const express = require('express');
const app = express();

app.use(express.json());

// GET all
app.get('/api/items', async (req, res) => {
  try {
    const items = await getAll();
    res.json(items);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// GET one
app.get('/api/items/:id', async (req, res) => {
  try {
    const item = await getById(parseInt(req.params.id));
    if (!item) {
      return res.status(404).json({ error: 'Item not found' });
    }
    res.json(item);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// POST create
app.post('/api/items', async (req, res) => {
  try {
    const item = await create(req.body);
    res.status(201).json(item);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// PUT update
app.put('/api/items/:id', async (req, res) => {
  try {
    const item = await update(parseInt(req.params.id), req.body);
    res.json(item);
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

// DELETE
app.delete('/api/items/:id', async (req, res) => {
  try {
    await remove(parseInt(req.params.id));
    res.status(204).send();
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

**Limitations:**
- Not suitable for high concurrency
- No transactions
- File locking issues
- Performance degrades with large datasets
- No query capabilities

**When to Use:**
- Prototyping
- Small applications
- Configuration storage
- Development/testing

---


## HTTP and Web Servers

### Q19. How do you create an HTTP server in Node.js? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Backend, HTTP, Web Server

**Answer:**

Node.js provides the built-in `http` module to create HTTP servers.

**Basic HTTP Server:**
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, Node.js!');
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});
```

**Handling Different Routes:**
```javascript
const http = require('http');
const url = require('url');

const server = http.createServer((req, res) => {
  const parsedUrl = url.parse(req.url, true);
  const path = parsedUrl.pathname;
  const method = req.method;

  if (path === '/' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>Home Page</h1>');
  } else if (path === '/api/users' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify([{ id: 1, name: 'John' }]));
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not Found');
  }
});

server.listen(3000);
```

**Handling POST Requests:**
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.method === 'POST') {
    let body = '';
    
    req.on('data', chunk => {
      body += chunk.toString();
    });
    
    req.on('end', () => {
      const data = JSON.parse(body);
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify({ received: data }));
    });
  } else {
    res.writeHead(405, { 'Content-Type': 'text/plain' });
    res.end('Method Not Allowed');
  }
});

server.listen(3000);
```

---

## Express.js Framework

### Q20. What is Express.js and how do you set it up? (Easy)

**Difficulty:** Basic  
**Role:** Junior Developer  
**Tags:** Programming, Backend, Express, Web Framework

**Answer:**

Express.js is a minimal and flexible Node.js web application framework that provides a robust set of features for web and mobile applications.

**Installation:**
```bash
npm init -y
npm install express
```

**Basic Setup:**
```javascript
const express = require('express');
const app = express();
const PORT = 3000;

// Middleware
app.use(express.json());
app.use(express.urlencoded({ extended: true }));

// Routes
app.get('/', (req, res) => {
  res.send('Hello, Express!');
});

app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

**Key Features:**
- Routing
- Middleware support
- Template engines
- Static file serving
- Error handling

---

### Q21. How do you handle routing in Express.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Express, Routing, Web

**Answer:**

Express provides powerful routing capabilities for handling different HTTP methods and URL patterns.

**Basic Routes:**
```javascript
const express = require('express');
const app = express();

// GET route
app.get('/users', (req, res) => {
  res.json([{ id: 1, name: 'John' }]);
});

// POST route
app.post('/users', (req, res) => {
  const user = req.body;
  res.status(201).json(user);
});

// PUT route
app.put('/users/:id', (req, res) => {
  const { id } = req.params;
  const updates = req.body;
  res.json({ id, ...updates });
});

// DELETE route
app.delete('/users/:id', (req, res) => {
  res.status(204).send();
});
```

**Route Parameters:**
```javascript
// Single parameter
app.get('/users/:id', (req, res) => {
  const { id } = req.params;
  res.json({ userId: id });
});

// Multiple parameters
app.get('/users/:userId/posts/:postId', (req, res) => {
  const { userId, postId } = req.params;
  res.json({ userId, postId });
});

// Query parameters
app.get('/search', (req, res) => {
  const { q, page } = req.query;
  res.json({ query: q, page });
});
```

**Route Handlers:**
```javascript
// Multiple handlers
app.get('/example',
  (req, res, next) => {
    console.log('First handler');
    next();
  },
  (req, res) => {
    res.send('Second handler');
  }
);

// Array of handlers
const middleware1 = (req, res, next) => {
  console.log('Middleware 1');
  next();
};

const middleware2 = (req, res, next) => {
  console.log('Middleware 2');
  next();
};

app.get('/example', [middleware1, middleware2], (req, res) => {
  res.send('Done');
});
```

**Router Module:**
```javascript
// routes/users.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.json([{ id: 1, name: 'John' }]);
});

router.get('/:id', (req, res) => {
  res.json({ id: req.params.id });
});

module.exports = router;

// app.js
const express = require('express');
const userRoutes = require('./routes/users');

const app = express();
app.use('/api/users', userRoutes);
```

---

## Middleware

### Q22. What is middleware in Express.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Express, Middleware, Web

**Answer:**

Middleware functions are functions that have access to the request object (req), response object (res), and the next middleware function in the application's request-response cycle.

**Basic Middleware:**
```javascript
const express = require('express');
const app = express();

// Custom middleware
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.path} - ${new Date()}`);
  next(); // Pass control to next middleware
};

app.use(logger);

app.get('/', (req, res) => {
  res.send('Hello');
});
```

**Middleware Types:**

**1. Application-level Middleware:**
```javascript
app.use((req, res, next) => {
  console.log('Application middleware');
  next();
});
```

**2. Router-level Middleware:**
```javascript
const router = express.Router();
router.use((req, res, next) => {
  console.log('Router middleware');
  next();
});
```

**3. Error-handling Middleware:**
```javascript
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```

**4. Built-in Middleware:**
```javascript
app.use(express.json());        // Parse JSON bodies
app.use(express.urlencoded());  // Parse URL-encoded bodies
app.use(express.static('public')); // Serve static files
```

**5. Third-party Middleware:**
```javascript
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');

app.use(cors());
app.use(helmet());
app.use(morgan('combined'));
```

**Common Middleware Examples:**

**Authentication Middleware:**
```javascript
const authenticate = (req, res, next) => {
  const token = req.headers.authorization;
  
  if (!token) {
    return res.status(401).json({ error: 'Unauthorized' });
  }
  
  // Verify token
  try {
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};

app.get('/protected', authenticate, (req, res) => {
  res.json({ message: 'Protected route', user: req.user });
});
```

**Validation Middleware:**
```javascript
const validateUser = (req, res, next) => {
  const { name, email } = req.body;
  
  if (!name || !email) {
    return res.status(400).json({ error: 'Name and email required' });
  }
  
  if (!email.includes('@')) {
    return res.status(400).json({ error: 'Invalid email' });
  }
  
  next();
};

app.post('/users', validateUser, (req, res) => {
  // Create user
});
```

---

## Database Connections

### Q23. How do you connect to MongoDB in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Database, MongoDB, I/O Operations

**Answer:**

MongoDB can be connected using the official `mongodb` driver or `mongoose` ODM (Object Document Mapper).

**Using MongoDB Native Driver:**
```javascript
const { MongoClient } = require('mongodb');

const uri = 'mongodb://localhost:27017';
const client = new MongoClient(uri);

async function connect() {
  try {
    await client.connect();
    console.log('Connected to MongoDB');
    
    const db = client.db('mydb');
    const collection = db.collection('users');
    
    // Insert
    await collection.insertOne({ name: 'John', age: 30 });
    
    // Find
    const users = await collection.find({}).toArray();
    console.log(users);
    
  } catch (error) {
    console.error('Error:', error);
  } finally {
    await client.close();
  }
}

connect();
```

**Using Mongoose:**
```javascript
const mongoose = require('mongoose');

// Connect
mongoose.connect('mongodb://localhost:27017/mydb', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});

// Connection events
mongoose.connection.on('connected', () => {
  console.log('Mongoose connected');
});

mongoose.connection.on('error', (err) => {
  console.error('Mongoose error:', err);
});

// Define schema
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number
});

// Create model
const User = mongoose.model('User', userSchema);

// Usage
async function createUser() {
  const user = new User({
    name: 'John',
    email: 'john@example.com',
    age: 30
  });
  
  await user.save();
  console.log('User created');
}
```

**Connection with Environment Variables:**
```javascript
require('dotenv').config();

mongoose.connect(process.env.MONGODB_URI, {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

---

### Q24. How do you connect to PostgreSQL in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Database, PostgreSQL, I/O Operations

**Answer:**

PostgreSQL can be connected using `pg` (node-postgres) library.

**Basic Connection:**
```javascript
const { Pool } = require('pg');

const pool = new Pool({
  user: 'postgres',
  host: 'localhost',
  database: 'mydb',
  password: 'password',
  port: 5432,
});

// Query
async function getUsers() {
  try {
    const result = await pool.query('SELECT * FROM users');
    return result.rows;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}
```

**Connection with Environment Variables:**
```javascript
require('dotenv').config();

const pool = new Pool({
  connectionString: process.env.DATABASE_URL,
  ssl: process.env.NODE_ENV === 'production' ? { rejectUnauthorized: false } : false
});
```

**Using Client (Single Connection):**
```javascript
const { Client } = require('pg');

const client = new Client({
  user: 'postgres',
  host: 'localhost',
  database: 'mydb',
  password: 'password',
  port: 5432,
});

async function connect() {
  await client.connect();
  
  const result = await client.query('SELECT * FROM users');
  console.log(result.rows);
  
  await client.end();
}

connect();
```

**Transaction:**
```javascript
const client = await pool.connect();

try {
  await client.query('BEGIN');
  
  await client.query('INSERT INTO users (name) VALUES ($1)', ['John']);
  await client.query('INSERT INTO posts (user_id, title) VALUES ($1, $2)', [1, 'Post 1']);
  
  await client.query('COMMIT');
} catch (error) {
  await client.query('ROLLBACK');
  throw error;
} finally {
  client.release();
}
```

---

### Q25. How do you connect to MySQL in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Database, MySQL, I/O Operations

**Answer:**

MySQL can be connected using `mysql2` library (recommended) or `mysql`.

**Using mysql2:**
```javascript
const mysql = require('mysql2/promise');

// Create connection pool
const pool = mysql.createPool({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'mydb',
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});

// Query
async function getUsers() {
  try {
    const [rows] = await pool.execute('SELECT * FROM users');
    return rows;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}

// Insert
async function createUser(name, email) {
  try {
    const [result] = await pool.execute(
      'INSERT INTO users (name, email) VALUES (?, ?)',
      [name, email]
    );
    return result.insertId;
  } catch (error) {
    console.error('Error:', error);
    throw error;
  }
}
```

**Using Connection:**
```javascript
const mysql = require('mysql2/promise');

async function connect() {
  const connection = await mysql.createConnection({
    host: 'localhost',
    user: 'root',
    password: 'password',
    database: 'mydb'
  });
  
  const [rows] = await connection.execute('SELECT * FROM users');
  console.log(rows);
  
  await connection.end();
}

connect();
```

**Transaction:**
```javascript
const connection = await mysql.createConnection({
  host: 'localhost',
  user: 'root',
  password: 'password',
  database: 'mydb'
});

try {
  await connection.beginTransaction();
  
  await connection.execute('INSERT INTO users (name) VALUES (?)', ['John']);
  await connection.execute('INSERT INTO posts (user_id, title) VALUES (?, ?)', [1, 'Post 1']);
  
  await connection.commit();
} catch (error) {
  await connection.rollback();
  throw error;
} finally {
  await connection.end();
}
```

---

## ORM and Query Builders

### Q26. What is an ORM and how do you use Sequelize? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Database, ORM, Sequelize

**Answer:**

ORM (Object-Relational Mapping) allows you to interact with databases using objects instead of SQL queries.

**Sequelize Setup:**
```bash
npm install sequelize
npm install pg pg-hstore  # For PostgreSQL
npm install mysql2        # For MySQL
npm install sqlite3       # For SQLite
```

**Basic Setup:**
```javascript
const { Sequelize, DataTypes } = require('sequelize');

const sequelize = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'postgres'
});

// Test connection
async function testConnection() {
  try {
    await sequelize.authenticate();
    console.log('Connection established');
  } catch (error) {
    console.error('Unable to connect:', error);
  }
}

testConnection();
```

**Define Models:**
```javascript
const User = sequelize.define('User', {
  id: {
    type: DataTypes.INTEGER,
    primaryKey: true,
    autoIncrement: true
  },
  name: {
    type: DataTypes.STRING,
    allowNull: false
  },
  email: {
    type: DataTypes.STRING,
    unique: true,
    allowNull: false
  },
  age: {
    type: DataTypes.INTEGER
  }
}, {
  tableName: 'users',
  timestamps: true
});
```

**CRUD Operations:**
```javascript
// Create
const user = await User.create({
  name: 'John',
  email: 'john@example.com',
  age: 30
});

// Read
const users = await User.findAll();
const user = await User.findByPk(1);
const user = await User.findOne({ where: { email: 'john@example.com' } });

// Update
await User.update(
  { name: 'Jane' },
  { where: { id: 1 } }
);

// Delete
await User.destroy({ where: { id: 1 } });
```

**Associations:**
```javascript
// One-to-Many
User.hasMany(Post, { foreignKey: 'userId' });
Post.belongsTo(User, { foreignKey: 'userId' });

// Many-to-Many
User.belongsToMany(Project, { through: 'UserProjects' });
Project.belongsToMany(User, { through: 'UserProjects' });
```

---

### Q27. How do you use Mongoose as an ODM? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Database, MongoDB, Mongoose, ODM

**Answer:**

Mongoose is an ODM (Object Document Mapper) for MongoDB, providing schema-based solution.

**Setup:**
```bash
npm install mongoose
```

**Connection:**
```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mydb', {
  useNewUrlParser: true,
  useUnifiedTopology: true
});
```

**Define Schema:**
```javascript
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  age: {
    type: Number,
    min: 0
  },
  createdAt: {
    type: Date,
    default: Date.now
  }
});

// Create model
const User = mongoose.model('User', userSchema);
```

**CRUD Operations:**
```javascript
// Create
const user = new User({
  name: 'John',
  email: 'john@example.com',
  age: 30
});
await user.save();

// Or
const user = await User.create({
  name: 'John',
  email: 'john@example.com',
  age: 30
});

// Read
const users = await User.find();
const user = await User.findById(id);
const user = await User.findOne({ email: 'john@example.com' });

// Update
await User.findByIdAndUpdate(id, { name: 'Jane' });
await User.updateOne({ _id: id }, { name: 'Jane' });

// Delete
await User.findByIdAndDelete(id);
await User.deleteOne({ _id: id });
```

**Relationships:**
```javascript
// One-to-Many
const postSchema = new mongoose.Schema({
  title: String,
  content: String,
  author: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User'
  }
});

const Post = mongoose.model('Post', postSchema);

// Populate
const post = await Post.findById(id).populate('author');
```

---


## Database Migrations

### Q28. How do you handle database migrations in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Database, Migrations, ORM

**Answer:**

Database migrations help manage schema changes over time in a version-controlled manner.

**Using Sequelize Migrations:**
```bash
# Install Sequelize CLI
npm install --save-dev sequelize-cli

# Initialize
npx sequelize-cli init

# Create migration
npx sequelize-cli migration:generate --name create-users-table
```

**Migration File:**
```javascript
// migrations/20240101000000-create-users-table.js
'use strict';

module.exports = {
  async up(queryInterface, Sequelize) {
    await queryInterface.createTable('users', {
      id: {
        allowNull: false,
        autoIncrement: true,
        primaryKey: true,
        type: Sequelize.INTEGER
      },
      name: {
        type: Sequelize.STRING,
        allowNull: false
      },
      email: {
        type: Sequelize.STRING,
        unique: true,
        allowNull: false
      },
      createdAt: {
        allowNull: false,
        type: Sequelize.DATE
      },
      updatedAt: {
        allowNull: false,
        type: Sequelize.DATE
      }
    });
  },

  async down(queryInterface, Sequelize) {
    await queryInterface.dropTable('users');
  }
};
```

**Running Migrations:**
```bash
# Run migrations
npx sequelize-cli db:migrate

# Rollback
npx sequelize-cli db:migrate:undo

# Rollback all
npx sequelize-cli db:migrate:undo:all
```

**Using Knex Migrations:**
```bash
npm install knex
npm install pg  # or mysql2, sqlite3

# Initialize
npx knex init

# Create migration
npx knex migrate:make create_users_table
```

**Knex Migration:**
```javascript
// migrations/20240101000000_create_users_table.js
exports.up = function(knex) {
  return knex.schema.createTable('users', function(table) {
    table.increments('id').primary();
    table.string('name').notNullable();
    table.string('email').unique().notNullable();
    table.timestamps(true, true);
  });
};

exports.down = function(knex) {
  return knex.schema.dropTable('users');
};
```

**Running Knex Migrations:**
```bash
# Run migrations
npx knex migrate:latest

# Rollback
npx knex migrate:rollback
```

**Best Practices:**
- Always write reversible migrations
- Test migrations on development first
- Use transactions when possible
- Keep migrations small and focused
- Never edit existing migrations

---

## Message Brokers

### Q29. How do you connect to RabbitMQ in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Message Broker, RabbitMQ, I/O Operations

**Answer:**

RabbitMQ is a message broker that implements AMQP (Advanced Message Queuing Protocol).

**Installation:**
```bash
npm install amqplib
```

**Publisher (Producer):**
```javascript
const amqp = require('amqplib');

async function publishMessage() {
  try {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    
    const queue = 'tasks';
    const message = 'Hello RabbitMQ!';
    
    // Assert queue exists
    await channel.assertQueue(queue, {
      durable: true  // Queue survives broker restart
    });
    
    // Send message
    channel.sendToQueue(queue, Buffer.from(message), {
      persistent: true  // Message survives broker restart
    });
    
    console.log(`Sent: ${message}`);
    
    setTimeout(() => {
      connection.close();
      process.exit(0);
    }, 500);
  } catch (error) {
    console.error('Error:', error);
  }
}

publishMessage();
```

**Consumer (Subscriber):**
```javascript
const amqp = require('amqplib');

async function consumeMessages() {
  try {
    const connection = await amqp.connect('amqp://localhost');
    const channel = await connection.createChannel();
    
    const queue = 'tasks';
    
    await channel.assertQueue(queue, {
      durable: true
    });
    
    // Prefetch: Only send one message at a time
    channel.prefetch(1);
    
    console.log('Waiting for messages...');
    
    channel.consume(queue, (msg) => {
      if (msg !== null) {
        const content = msg.content.toString();
        console.log(`Received: ${content}`);
        
        // Acknowledge message
        channel.ack(msg);
      }
    });
  } catch (error) {
    console.error('Error:', error);
  }
}

consumeMessages();
```

**Work Queue Pattern:**
```javascript
// Publisher
const channel = await connection.createChannel();
const queue = 'task_queue';

for (let i = 0; i < 10; i++) {
  const message = `Task ${i}`;
  channel.sendToQueue(queue, Buffer.from(message), {
    persistent: true
  });
  console.log(`Sent: ${message}`);
}
```

**Pub/Sub Pattern:**
```javascript
// Publisher
const exchange = 'logs';
await channel.assertExchange(exchange, 'fanout', { durable: false });

const message = 'Hello World!';
channel.publish(exchange, '', Buffer.from(message));
console.log(`Sent: ${message}`);

// Consumer
const exchange = 'logs';
await channel.assertExchange(exchange, 'fanout', { durable: false });

const q = await channel.assertQueue('', { exclusive: true });
channel.bindQueue(q.queue, exchange, '');

channel.consume(q.queue, (msg) => {
  if (msg) {
    console.log(`Received: ${msg.content.toString()}`);
  }
}, { noAck: true });
```

---

### Q30. How do you connect to Apache Kafka in Node.js? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Message Broker, Kafka, I/O Operations

**Answer:**

Apache Kafka is a distributed event streaming platform.

**Installation:**
```bash
npm install kafkajs
```

**Producer:**
```javascript
const { Kafka } = require('kafkajs');

const kafka = new Kafka({
  clientId: 'my-app',
  brokers: ['localhost:9092']
});

const producer = kafka.producer();

async function produceMessage() {
  await producer.connect();
  
  await producer.send({
    topic: 'test-topic',
    messages: [
      {
        key: 'key1',
        value: JSON.stringify({ message: 'Hello Kafka!' })
      }
    ]
  });
  
  await producer.disconnect();
}

produceMessage();
```

**Consumer:**
```javascript
const { Kafka } = require('kafkajs');

const kafka = new Kafka({
  clientId: 'my-app',
  brokers: ['localhost:9092']
});

const consumer = kafka.consumer({ groupId: 'test-group' });

async function consumeMessages() {
  await consumer.connect();
  await consumer.subscribe({ topic: 'test-topic', fromBeginning: true });
  
  await consumer.run({
    eachMessage: async ({ topic, partition, message }) => {
      console.log({
        topic,
        partition,
        offset: message.offset,
        value: message.value.toString()
      });
    }
  });
}

consumeMessages();
```

**Consumer Groups:**
```javascript
// Multiple consumers in same group share partitions
const consumer1 = kafka.consumer({ groupId: 'my-group' });
const consumer2 = kafka.consumer({ groupId: 'my-group' });

// Each consumer processes different partitions
```

---

## Caching with Redis

### Q31. How do you connect to Redis in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Caching, Redis, I/O Operations

**Answer:**

Redis is an in-memory data structure store used as a cache, database, and message broker.

**Installation:**
```bash
npm install redis
```

**Basic Connection:**
```javascript
const redis = require('redis');

const client = redis.createClient({
  host: 'localhost',
  port: 6379
});

client.on('error', (err) => {
  console.error('Redis Client Error', err);
});

client.on('connect', () => {
  console.log('Connected to Redis');
});

await client.connect();
```

**Basic Operations:**
```javascript
// String operations
await client.set('key', 'value');
const value = await client.get('key');

// Set expiration
await client.setEx('key', 3600, 'value'); // Expires in 1 hour

// Check existence
const exists = await client.exists('key');

// Delete
await client.del('key');
```

**Hash Operations:**
```javascript
// Set hash fields
await client.hSet('user:1', {
  name: 'John',
  email: 'john@example.com',
  age: '30'
});

// Get hash field
const name = await client.hGet('user:1', 'name');

// Get all hash fields
const user = await client.hGetAll('user:1');

// Delete hash field
await client.hDel('user:1', 'age');
```

**List Operations:**
```javascript
// Push to list
await client.lPush('tasks', 'task1');
await client.rPush('tasks', 'task2');

// Get list
const tasks = await client.lRange('tasks', 0, -1);

// Pop from list
const task = await client.lPop('tasks');
```

**Set Operations:**
```javascript
// Add to set
await client.sAdd('tags', 'javascript', 'nodejs');

// Get set members
const tags = await client.sMembers('tags');

// Check membership
const isMember = await client.sIsMember('tags', 'javascript');
```

**Caching Example:**
```javascript
async function getCachedUser(userId) {
  const cacheKey = `user:${userId}`;
  
  // Try cache first
  const cached = await client.get(cacheKey);
  if (cached) {
    return JSON.parse(cached);
  }
  
  // Fetch from database
  const user = await db.users.findById(userId);
  
  // Store in cache (expire in 1 hour)
  await client.setEx(cacheKey, 3600, JSON.stringify(user));
  
  return user;
}
```

**Session Storage:**
```javascript
async function setSession(sessionId, data) {
  await client.setEx(`session:${sessionId}`, 3600, JSON.stringify(data));
}

async function getSession(sessionId) {
  const data = await client.get(`session:${sessionId}`);
  return data ? JSON.parse(data) : null;
}
```

---

## Authentication

### Q32. How do you implement JWT authentication in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Authentication, Security, JWT

**Answer:**

JWT (JSON Web Tokens) is a stateless authentication mechanism.

**Installation:**
```bash
npm install jsonwebtoken bcryptjs
```

**Login Route:**
```javascript
const jwt = require('jsonwebtoken');
const bcrypt = require('bcryptjs');

app.post('/api/login', async (req, res) => {
  try {
    const { email, password } = req.body;
    
    // Find user
    const user = await User.findOne({ email });
    if (!user) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Verify password
    const isValid = await bcrypt.compare(password, user.password);
    if (!isValid) {
      return res.status(401).json({ error: 'Invalid credentials' });
    }
    
    // Generate token
    const token = jwt.sign(
      { userId: user.id, email: user.email },
      process.env.JWT_SECRET,
      { expiresIn: '24h' }
    );
    
    res.json({ token, user: { id: user.id, email: user.email } });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});
```

**Authentication Middleware:**
```javascript
const authenticate = (req, res, next) => {
  try {
    const token = req.headers.authorization?.split(' ')[1]; // Bearer TOKEN
    
    if (!token) {
      return res.status(401).json({ error: 'No token provided' });
    }
    
    const decoded = jwt.verify(token, process.env.JWT_SECRET);
    req.user = decoded;
    next();
  } catch (error) {
    res.status(401).json({ error: 'Invalid token' });
  }
};

// Protected route
app.get('/api/profile', authenticate, (req, res) => {
  res.json({ user: req.user });
});
```

**Refresh Tokens:**
```javascript
// Generate refresh token
const refreshToken = jwt.sign(
  { userId: user.id },
  process.env.REFRESH_SECRET,
  { expiresIn: '7d' }
);

// Store refresh token
await RefreshToken.create({ userId: user.id, token: refreshToken });

// Refresh endpoint
app.post('/api/refresh', async (req, res) => {
  const { refreshToken } = req.body;
  
  try {
    const decoded = jwt.verify(refreshToken, process.env.REFRESH_SECRET);
    const stored = await RefreshToken.findOne({ 
      userId: decoded.userId, 
      token: refreshToken 
    });
    
    if (!stored) {
      return res.status(401).json({ error: 'Invalid refresh token' });
    }
    
    const newToken = jwt.sign(
      { userId: decoded.userId },
      process.env.JWT_SECRET,
      { expiresIn: '24h' }
    );
    
    res.json({ token: newToken });
  } catch (error) {
    res.status(401).json({ error: 'Invalid refresh token' });
  }
});
```

---

### Q33. How do you implement OAuth authentication? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Authentication, OAuth, Security

**Answer:**

OAuth allows users to authenticate using third-party providers (Google, GitHub, etc.).

**Using Passport.js:**
```bash
npm install passport passport-google-oauth20
```

**Setup:**
```javascript
const passport = require('passport');
const GoogleStrategy = require('passport-google-oauth20').Strategy;

passport.use(new GoogleStrategy({
  clientID: process.env.GOOGLE_CLIENT_ID,
  clientSecret: process.env.GOOGLE_CLIENT_SECRET,
  callbackURL: '/auth/google/callback'
}, async (accessToken, refreshToken, profile, done) => {
  try {
    let user = await User.findOne({ googleId: profile.id });
    
    if (!user) {
      user = await User.create({
        googleId: profile.id,
        name: profile.displayName,
        email: profile.emails[0].value
      });
    }
    
    return done(null, user);
  } catch (error) {
    return done(error, null);
  }
}));

// Serialize user
passport.serializeUser((user, done) => {
  done(null, user.id);
});

passport.deserializeUser(async (id, done) => {
  const user = await User.findById(id);
  done(null, user);
});
```

**Routes:**
```javascript
app.get('/auth/google',
  passport.authenticate('google', { scope: ['profile', 'email'] })
);

app.get('/auth/google/callback',
  passport.authenticate('google', { failureRedirect: '/login' }),
  (req, res) => {
    res.redirect('/dashboard');
  }
);
```

---

## Authorization

### Q34. How do you implement role-based access control (RBAC)? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Authorization, Security, RBAC

**Answer:**

RBAC restricts access based on user roles.

**Role Middleware:**
```javascript
const authorize = (...roles) => {
  return (req, res, next) => {
    if (!req.user) {
      return res.status(401).json({ error: 'Unauthorized' });
    }
    
    if (!roles.includes(req.user.role)) {
      return res.status(403).json({ error: 'Forbidden' });
    }
    
    next();
  };
};

// Usage
app.get('/api/admin/users', 
  authenticate, 
  authorize('admin'), 
  async (req, res) => {
    const users = await User.find();
    res.json(users);
  }
);
```

**Permission-Based:**
```javascript
const checkPermission = (permission) => {
  return (req, res, next) => {
    if (!req.user.permissions.includes(permission)) {
      return res.status(403).json({ error: 'Insufficient permissions' });
    }
    next();
  };
};

app.delete('/api/users/:id',
  authenticate,
  checkPermission('users:delete'),
  async (req, res) => {
    await User.findByIdAndDelete(req.params.id);
    res.status(204).send();
  }
);
```

---

## Security Practices

### Q35. What are the best security practices for Node.js applications? (Hard)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Security, Best Practices

**Answer:**

**1. Input Validation:**
```javascript
const { body, validationResult } = require('express-validator');

app.post('/api/users',
  body('email').isEmail(),
  body('password').isLength({ min: 8 }),
  async (req, res) => {
    const errors = validationResult(req);
    if (!errors.isEmpty()) {
      return res.status(400).json({ errors: errors.array() });
    }
    // Process request
  }
);
```

**2. SQL Injection Prevention:**
```javascript
// Use parameterized queries
await db.query('SELECT * FROM users WHERE id = $1', [userId]);

// Never do this:
// await db.query(`SELECT * FROM users WHERE id = ${userId}`);
```

**3. XSS Prevention:**
```javascript
const helmet = require('helmet');
app.use(helmet());

// Sanitize user input
const sanitize = require('sanitize-html');
const clean = sanitize(userInput);
```

**4. Rate Limiting:**
```javascript
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // Limit each IP to 100 requests per windowMs
});

app.use('/api/', limiter);
```

**5. HTTPS:**
```javascript
const https = require('https');
const fs = require('fs');

const options = {
  key: fs.readFileSync('key.pem'),
  cert: fs.readFileSync('cert.pem')
};

https.createServer(options, app).listen(443);
```

**6. Environment Variables:**
```javascript
require('dotenv').config();

// Never hardcode secrets
const secret = process.env.JWT_SECRET;
```

**7. CORS:**
```javascript
const cors = require('cors');

app.use(cors({
  origin: process.env.ALLOWED_ORIGINS.split(','),
  credentials: true
}));
```

**8. Security Headers:**
```javascript
app.use(helmet({
  contentSecurityPolicy: {
    directives: {
      defaultSrc: ["'self'"],
      styleSrc: ["'self'", "'unsafe-inline'"]
    }
  }
}));
```

---


## Error Handling

### Q36. How do you handle errors in Node.js applications? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Error Handling, Best Practices

**Answer:**

Proper error handling is crucial for robust applications.

**Try-Catch for Async:**
```javascript
async function fetchUser(id) {
  try {
    const user = await User.findById(id);
    if (!user) {
      throw new Error('User not found');
    }
    return user;
  } catch (error) {
    console.error('Error fetching user:', error);
    throw error;
  }
}
```

**Error Middleware:**
```javascript
// Error handling middleware (must be last)
app.use((err, req, res, next) => {
  console.error(err.stack);
  
  res.status(err.status || 500).json({
    error: {
      message: err.message || 'Internal Server Error',
      ...(process.env.NODE_ENV === 'development' && { stack: err.stack })
    }
  });
});
```

**Custom Error Classes:**
```javascript
class AppError extends Error {
  constructor(message, statusCode) {
    super(message);
    this.statusCode = statusCode;
    this.status = `${statusCode}`.startsWith('4') ? 'fail' : 'error';
    this.isOperational = true;
    
    Error.captureStackTrace(this, this.constructor);
  }
}

// Usage
throw new AppError('User not found', 404);
```

**Async Error Wrapper:**
```javascript
const catchAsync = (fn) => {
  return (req, res, next) => {
    fn(req, res, next).catch(next);
  };
};

// Usage
app.get('/api/users/:id', catchAsync(async (req, res) => {
  const user = await User.findById(req.params.id);
  if (!user) {
    throw new AppError('User not found', 404);
  }
  res.json(user);
}));
```

**Unhandled Rejections:**
```javascript
process.on('unhandledRejection', (err) => {
  console.error('UNHANDLED REJECTION! Shutting down...');
  console.error(err.name, err.message);
  server.close(() => {
    process.exit(1);
  });
});
```

---

## Testing

### Q37. How do you write tests in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Junior Developer, Senior Developer  
**Tags:** Programming, Backend, Testing, Jest, Mocha

**Answer:**

Testing ensures code quality and prevents regressions.

**Using Jest:**
```bash
npm install --save-dev jest
```

**Unit Test:**
```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = { add };

// math.test.js
const { add } = require('./math');

describe('Math functions', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
  });
  
  test('adds negative numbers', () => {
    expect(add(-1, -2)).toBe(-3);
  });
});
```

**API Testing:**
```javascript
const request = require('supertest');
const app = require('../app');

describe('User API', () => {
  test('GET /api/users', async () => {
    const response = await request(app)
      .get('/api/users')
      .expect(200);
    
    expect(response.body).toBeInstanceOf(Array);
  });
  
  test('POST /api/users', async () => {
    const newUser = {
      name: 'John',
      email: 'john@example.com'
    };
    
    const response = await request(app)
      .post('/api/users')
      .send(newUser)
      .expect(201);
    
    expect(response.body).toHaveProperty('id');
    expect(response.body.name).toBe(newUser.name);
  });
});
```

**Using Mocha and Chai:**
```bash
npm install --save-dev mocha chai
```

```javascript
const { expect } = require('chai');
const request = require('supertest');
const app = require('../app');

describe('User API', () => {
  it('should get all users', async () => {
    const res = await request(app)
      .get('/api/users')
      .expect(200);
    
    expect(res.body).to.be.an('array');
  });
});
```

**Test Database Setup:**
```javascript
const mongoose = require('mongoose');

beforeAll(async () => {
  await mongoose.connect(process.env.TEST_DATABASE_URL);
});

afterAll(async () => {
  await mongoose.connection.close();
});

beforeEach(async () => {
  await User.deleteMany({});
});
```

---

## Server-Side Rendering

### Q38. How do you implement server-side rendering in Node.js? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Server-Side Rendering, SSR, Web

**Answer:**

SSR renders HTML on the server before sending to client.

**Using EJS Template Engine:**
```bash
npm install ejs
```

```javascript
const express = require('express');
const app = express();

app.set('view engine', 'ejs');
app.set('views', './views');

app.get('/', async (req, res) => {
  const users = await User.find();
  res.render('index', { users, title: 'Home Page' });
});
```

**EJS Template:**
```html
<!-- views/index.ejs -->
<!DOCTYPE html>
<html>
<head>
  <title><%= title %></title>
</head>
<body>
  <h1>Users</h1>
  <ul>
    <% users.forEach(user => { %>
      <li><%= user.name %></li>
    <% }); %>
  </ul>
</body>
</html>
```

**Using Handlebars:**
```bash
npm install express-handlebars
```

```javascript
const exphbs = require('express-handlebars');

app.engine('handlebars', exphbs());
app.set('view engine', 'handlebars');

app.get('/', async (req, res) => {
  const users = await User.find();
  res.render('index', { users });
});
```

**Using Next.js (React SSR):**
```javascript
// pages/index.js
export async function getServerSideProps() {
  const users = await fetchUsers();
  return {
    props: { users }
  };
}

export default function Home({ users }) {
  return (
    <div>
      {users.map(user => (
        <div key={user.id}>{user.name}</div>
      ))}
    </div>
  );
}
```

**SSR vs CSR:**
- **SSR:** Better SEO, faster initial load, server load
- **CSR:** Faster navigation, less server load, SEO challenges

---

## Performance Optimization

### Q39. How do you optimize Node.js application performance? (Hard)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Performance, Optimization

**Answer:**

**1. Use Clustering:**
```javascript
const cluster = require('cluster');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  
  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }
  
  cluster.on('exit', (worker) => {
    console.log(`Worker ${worker.process.pid} died`);
    cluster.fork();
  });
} else {
  // Worker process
  const app = require('./app');
  app.listen(3000);
}
```

**2. Use Worker Threads for CPU-intensive Tasks:**
```javascript
const { Worker } = require('worker_threads');

function runWorker(data) {
  return new Promise((resolve, reject) => {
    const worker = new Worker('./worker.js', {
      workerData: data
    });
    
    worker.on('message', resolve);
    worker.on('error', reject);
  });
}
```

**3. Enable Compression:**
```javascript
const compression = require('compression');
app.use(compression());
```

**4. Use Caching:**
```javascript
const redis = require('redis');
const client = redis.createClient();

async function getCachedData(key) {
  const cached = await client.get(key);
  if (cached) return JSON.parse(cached);
  
  const data = await fetchData();
  await client.setEx(key, 3600, JSON.stringify(data));
  return data;
}
```

**5. Database Query Optimization:**
```javascript
// Use indexes
await User.createIndex({ email: 1 });

// Use select to limit fields
const users = await User.find().select('name email');

// Use pagination
const page = 1;
const limit = 10;
const users = await User.find()
  .skip((page - 1) * limit)
  .limit(limit);
```

**6. Use Connection Pooling:**
```javascript
const pool = new Pool({
  max: 20,
  idleTimeoutMillis: 30000,
  connectionTimeoutMillis: 2000
});
```

**7. Enable HTTP/2:**
```javascript
const http2 = require('http2');
const fs = require('fs');

const server = http2.createSecureServer({
  key: fs.readFileSync('key.pem'),
  cert: fs.readFileSync('cert.pem')
});
```

---

## Deployment and DevOps

### Q40. How do you deploy a Node.js application? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Deployment, DevOps, Docker

**Answer:**

**1. Using PM2:**
```bash
npm install -g pm2

# Start application
pm2 start app.js

# Start with ecosystem file
pm2 start ecosystem.config.js

# Monitor
pm2 monit

# Logs
pm2 logs

# Restart
pm2 restart app

# Stop
pm2 stop app
```

**ecosystem.config.js:**
```javascript
module.exports = {
  apps: [{
    name: 'my-app',
    script: './app.js',
    instances: 4,
    exec_mode: 'cluster',
    env: {
      NODE_ENV: 'production',
      PORT: 3000
    }
  }]
};
```

**2. Using Docker:**
```dockerfile
# Dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

```bash
# Build
docker build -t my-app .

# Run
docker run -p 3000:3000 my-app
```

**3. Using Docker Compose:**
```yaml
# docker-compose.yml
version: '3.8'

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
    depends_on:
      - db
      - redis
  
  db:
    image: postgres:14
    environment:
      - POSTGRES_DB=mydb
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
  
  redis:
    image: redis:7-alpine
```

**4. Environment Variables:**
```bash
# .env
NODE_ENV=production
PORT=3000
DATABASE_URL=postgresql://...
JWT_SECRET=your-secret
```

**5. Health Checks:**
```javascript
app.get('/health', (req, res) => {
  res.json({
    status: 'ok',
    timestamp: new Date().toISOString(),
    uptime: process.uptime()
  });
});
```

---

## Advanced Topics

### Q41. What are streams in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Streams, I/O Operations

**Answer:**

Streams are objects that let you read/write data continuously.

**Types of Streams:**
1. **Readable:** Read data (fs.createReadStream)
2. **Writable:** Write data (fs.createWriteStream)
3. **Duplex:** Both read and write (net.Socket)
4. **Transform:** Duplex that can modify data (zlib.createGzip)

**Reading Large Files:**
```javascript
const fs = require('fs');

const readStream = fs.createReadStream('large-file.txt', {
  highWaterMark: 64 * 1024 // 64KB chunks
});

readStream.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes`);
});

readStream.on('end', () => {
  console.log('Finished reading');
});
```

**Piping:**
```javascript
const fs = require('fs');
const zlib = require('zlib');

fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
```

**Custom Transform Stream:**
```javascript
const { Transform } = require('stream');

class UpperCaseTransform extends Transform {
  _transform(chunk, encoding, callback) {
    this.push(chunk.toString().toUpperCase());
    callback();
  }
}

process.stdin
  .pipe(new UpperCaseTransform())
  .pipe(process.stdout);
```

---

### Q42. What is the Buffer class in Node.js? (Medium)

**Difficulty:** Intermediate  
**Role:** Senior Developer  
**Tags:** Programming, Backend, Buffer, I/O Operations

**Answer:**

Buffer is used to handle binary data directly in memory.

**Creating Buffers:**
```javascript
// From string
const buf1 = Buffer.from('Hello');
const buf2 = Buffer.from('Hello', 'utf8');

// Allocate
const buf3 = Buffer.alloc(10);
const buf4 = Buffer.allocUnsafe(10); // Faster but may contain old data

// From array
const buf5 = Buffer.from([0x48, 0x65, 0x6c, 0x6c, 0x6f]);
```

**Buffer Operations:**
```javascript
const buf = Buffer.from('Hello World');

console.log(buf.toString()); // 'Hello World'
console.log(buf.toString('hex')); // '48656c6c6f20576f726c64'
console.log(buf.length); // 11
console.log(buf[0]); // 72 (ASCII code for 'H')

// Slice
const slice = buf.slice(0, 5);
console.log(slice.toString()); // 'Hello'

// Copy
const buf2 = Buffer.alloc(5);
buf.copy(buf2, 0, 0, 5);
```

**Use Cases:**
- Reading binary files
- Network protocols
- Image processing
- Cryptography

---

### Q43. How do you handle child processes in Node.js? (Medium)

**Difficulty:** Advanced  
**Role:** Senior Developer, Architect  
**Tags:** Programming, Backend, Child Processes, Process Management

**Answer:**

Child processes allow running external commands and scripts.

**spawn:**
```javascript
const { spawn } = require('child_process');

const ls = spawn('ls', ['-la']);

ls.stdout.on('data', (data) => {
  console.log(`stdout: ${data}`);
});

ls.stderr.on('data', (data) => {
  console.error(`stderr: ${data}`);
});

ls.on('close', (code) => {
  console.log(`Process exited with code ${code}`);
});
```

**exec:**
```javascript
const { exec } = require('child_process');

exec('ls -la', (error, stdout, stderr) => {
  if (error) {
    console.error(`Error: ${error.message}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.error(`stderr: ${stderr}`);
});
```

**fork:**
```javascript
const { fork } = require('child_process');

const child = fork('child.js');

child.on('message', (msg) => {
  console.log('Message from child:', msg);
});

child.send({ hello: 'world' });
```

---

## Summary

This comprehensive guide covers all essential Node.js topics for interview preparation:

**Difficulty Levels:**
- **Basic:** Fundamentals, syntax, basic concepts
- **Intermediate:** Common patterns, frameworks, databases
- **Advanced:** Performance, architecture, complex scenarios

**Role Suitability:**
- **Junior Developer:** Basic to intermediate topics
- **Senior Developer:** All topics including advanced
- **Architect:** Advanced topics, system design, scalability

**Key Topics Covered:**
- Node.js fundamentals and architecture
- JavaScript basics (variables, constants, OOPs)
- Asynchronous programming (Promises, async/await)
- File I/O operations and streams
- HTTP servers and Express.js
- Database connections (MongoDB, PostgreSQL, MySQL)
- ORM and query builders (Sequelize, Mongoose)
- Database migrations
- CRUD operations (including static JSON files)
- Message brokers (RabbitMQ, Kafka)
- Caching with Redis
- Authentication (JWT, OAuth)
- Authorization (RBAC)
- Security best practices
- Error handling
- Testing
- Server-side rendering
- Performance optimization
- Deployment and DevOps
- Advanced topics (streams, buffers, child processes)

---

## References

- [Node.js Official Documentation](https://nodejs.org/docs/)
- [Express.js Documentation](https://expressjs.com/)
- [Node.js Roadmap](https://roadmap.sh/nodejs)
- [MongoDB Node.js Driver](https://www.mongodb.com/docs/drivers/node/)
- [Sequelize Documentation](https://sequelize.org/)
- [Redis Node.js Client](https://github.com/redis/node-redis)

---

*Last Updated: 2024*

*This guide is designed to be a comprehensive one-stop resource for Node.js interview preparation, covering all essential topics from basics to advanced concepts.*

