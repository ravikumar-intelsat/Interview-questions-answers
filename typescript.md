# TypeScript Interview Questions - Complete Guide

Based on the TypeScript Developer Roadmap from [roadmap.sh](https://roadmap.sh/typescript), this document covers interview questions for all topics in the TypeScript ecosystem.

---

## Table of Contents

1. [Introduction to TypeScript](#introduction-to-typescript)
2. [Basic Types](#basic-types)
3. [Variables and Type Annotations](#variables-and-type-annotations)
4. [Functions](#functions)
5. [Interfaces](#interfaces)
6. [Classes](#classes)
7. [Enums](#enums)
8. [Generics](#generics)
9. [Type Inference](#type-inference)
10. [Type Assertions](#type-assertions)
11. [Union and Intersection Types](#union-and-intersection-types)
12. [Type Aliases](#type-aliases)
13. [Modules and Namespaces](#modules-and-namespaces)
14. [Advanced Types](#advanced-types)
15. [Utility Types](#utility-types)
16. [Type Guards](#type-guards)
17. [Decorators](#decorators)
18. [Mixins](#mixins)
19. [Conditional Types](#conditional-types)
20. [Mapped Types](#mapped-types)
21. [Template Literal Types](#template-literal-types)
22. [TypeScript Configuration](#typescript-configuration)
23. [Error Handling](#error-handling)
24. [Best Practices](#best-practices)

---

## Introduction to TypeScript

### 1. What is TypeScript, and how does it differ from JavaScript?

**Answer:** TypeScript is a statically typed superset of JavaScript that compiles to plain JavaScript. It adds optional static type checking, interfaces, classes, generics, and other features to JavaScript. The main differences are:

- **Static Typing**: TypeScript provides compile-time type checking, while JavaScript is dynamically typed
- **Type Safety**: TypeScript catches errors during development, not at runtime
- **Enhanced IDE Support**: Better autocomplete, refactoring, and navigation
- **Compilation**: TypeScript must be compiled to JavaScript before execution
- **Backward Compatibility**: All valid JavaScript is valid TypeScript

**Example:**

```typescript
// JavaScript - No type checking
let message = "Hello, world!";
message = 42; // No error, but could cause issues later

// TypeScript - Type checking
let message: string = "Hello, world!";
message = 42; // Error: Type 'number' is not assignable to type 'string'
```

### 2. What are the advantages of using TypeScript over JavaScript?

**Answer:** The main advantages include:

- **Early Error Detection**: Catches errors at compile-time rather than runtime
- **Better Code Documentation**: Types serve as inline documentation
- **Improved IDE Support**: Enhanced autocomplete, IntelliSense, and refactoring
- **Easier Refactoring**: Type system helps identify all places that need updates
- **Better Team Collaboration**: Types make code more self-documenting
- **Scalability**: Easier to maintain large codebases
- **Modern JavaScript Features**: Access to latest ECMAScript features with type safety

**Example:**

```typescript
// TypeScript provides better IDE support
interface User {
  id: number;
  name: string;
  email: string;
}

function getUser(id: number): User {
  // IDE knows the return type and provides autocomplete
  return {
    id: id,
    name: "John Doe",
    email: "john@example.com"
  };
}

// Type checking prevents errors
const user = getUser(1);
console.log(user.nam); // Error: Property 'nam' does not exist. Did you mean 'name'?
```

### 3. How does TypeScript compile to JavaScript?

**Answer:** TypeScript uses a transpiler (TypeScript compiler - `tsc`) that:
1. Performs type checking
2. Removes all type annotations
3. Transpiles modern JavaScript features to target version
4. Generates source maps for debugging
5. Outputs plain JavaScript files

**Example:**

```typescript
// TypeScript source (example.ts)
function greet(name: string): string {
  return `Hello, ${name}!`;
}

// Compiled JavaScript (example.js)
function greet(name) {
  return "Hello, " + name + "!";
}
```

---

## Basic Types

### 4. What are the basic types in TypeScript?

**Answer:** TypeScript provides several basic types:

- `number`: Both integers and floating-point numbers
- `string`: Text data
- `boolean`: true or false
- `null`: Intentional absence of value
- `undefined`: Uninitialized variable
- `any`: Any type (disables type checking)
- `void`: Absence of a value (typically for functions)
- `never`: Represents values that never occur
- `object`: Non-primitive type
- `unknown`: Type-safe alternative to `any`

**Example:**

```typescript
let age: number = 30;
let name: string = "John";
let isActive: boolean = true;
let data: null = null;
let value: undefined = undefined;
let anything: any = "can be anything";
let nothing: void = undefined;
let neverValue: never; // Used for functions that never return

// Object type
let user: object = { name: "John", age: 30 };

// Unknown type (safer than any)
let userInput: unknown;
userInput = 5;
userInput = "hello";
// Need type checking before using
if (typeof userInput === "string") {
  console.log(userInput.toUpperCase());
}
```

### 5. What is the difference between `any` and `unknown` types?

**Answer:** Both `any` and `unknown` can hold any value, but `unknown` is type-safe:

- **`any`**: Disables all type checking, allows any operation without errors
- **`unknown`**: Requires type checking or type assertion before use, maintains type safety

**Example:**

```typescript
// any - no type checking
let valueAny: any = "hello";
valueAny.toUpperCase(); // OK, no error
valueAny.foo.bar; // OK, no error (but will fail at runtime)

// unknown - requires type checking
let valueUnknown: unknown = "hello";
// valueUnknown.toUpperCase(); // Error: Object is of type 'unknown'

// Must check type first
if (typeof valueUnknown === "string") {
  valueUnknown.toUpperCase(); // OK now
}

// Or use type assertion
(valueUnknown as string).toUpperCase(); // OK with assertion
```

### 6. What is the `never` type and when is it used?

**Answer:** The `never` type represents values that never occur. It's used for:

- Functions that never return (infinite loops, throw errors)
- Exhaustive checking in union types
- Functions that always throw exceptions

**Example:**

```typescript
// Function that never returns
function throwError(message: string): never {
  throw new Error(message);
}

// Function with infinite loop
function infiniteLoop(): never {
  while (true) {
    // never returns
  }
}

// Exhaustive checking
type Status = "success" | "error" | "loading";

function handleStatus(status: Status): string {
  switch (status) {
    case "success":
      return "Done";
    case "error":
      return "Failed";
    case "loading":
      return "Processing";
    default:
      // TypeScript ensures all cases are handled
      const exhaustiveCheck: never = status;
      return exhaustiveCheck;
  }
}
```

---

## Variables and Type Annotations

### 7. How do you declare variables with types in TypeScript?

**Answer:** TypeScript allows explicit type annotations using the colon syntax (`: type`) after the variable name. You can also rely on type inference.

**Example:**

```typescript
// Explicit type annotation
let name: string = "John";
let age: number = 30;
let isActive: boolean = true;

// Type inference (TypeScript infers the type)
let city = "New York"; // inferred as string
let count = 10; // inferred as number

// Multiple types (union)
let id: string | number = "123";
id = 456; // Also valid

// Arrays
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["John", "Jane"];

// Tuples
let tuple: [string, number] = ["hello", 42];
```

### 8. What is the difference between `let`, `const`, and `var` in TypeScript?

**Answer:** The differences are the same as in JavaScript, but TypeScript adds type checking:

- **`var`**: Function-scoped, hoisted, can be redeclared
- **`let`**: Block-scoped, not hoisted, cannot be redeclared, can be reassigned
- **`const`**: Block-scoped, not hoisted, cannot be redeclared or reassigned (but object properties can be mutated)

**Example:**

```typescript
// var - function scoped
function example1() {
  if (true) {
    var x: number = 10;
  }
  console.log(x); // 10 (accessible outside block)
}

// let - block scoped
function example2() {
  if (true) {
    let y: number = 20;
  }
  // console.log(y); // Error: y is not defined
}

// const - cannot reassign
const pi: number = 3.14;
// pi = 3.14159; // Error: Cannot assign to 'pi'

// But object properties can be mutated
const person = { name: "John", age: 30 };
person.age = 31; // OK
// person = { name: "Jane" }; // Error: Cannot assign to 'person'
```

---

## Functions

### 9. How do you define functions with typed parameters and return types?

**Answer:** TypeScript allows you to specify types for function parameters and return values using type annotations.

**Example:**

```typescript
// Function with typed parameters and return type
function add(x: number, y: number): number {
  return x + y;
}

// Function with optional parameter
function greet(name: string, title?: string): string {
  return title ? `Hello, ${title} ${name}` : `Hello, ${name}`;
}

// Function with default parameter
function multiply(a: number, b: number = 1): number {
  return a * b;
}

// Function with rest parameters
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}

// Arrow function
const subtract = (x: number, y: number): number => x - y;

// Function that returns void
function logMessage(message: string): void {
  console.log(message);
}

// Function that never returns
function throwError(): never {
  throw new Error("Something went wrong");
}
```

### 10. What are function overloads in TypeScript?

**Answer:** Function overloads allow a function to have multiple signatures with different parameter types or counts. TypeScript uses the overload signatures to check function calls.

**Example:**

```typescript
// Function overloads
function format(value: string): string;
function format(value: number): string;
function format(value: boolean): string;
function format(value: string | number | boolean): string {
  if (typeof value === "string") {
    return value.toUpperCase();
  } else if (typeof value === "number") {
    return value.toFixed(2);
  } else {
    return value ? "YES" : "NO";
  }
}

// Usage
format("hello"); // Returns "HELLO"
format(42); // Returns "42.00"
format(true); // Returns "YES"
```

### 11. What are optional and default parameters in TypeScript?

**Answer:** Optional parameters are marked with `?` and can be omitted. Default parameters have a default value assigned.

**Example:**

```typescript
// Optional parameter
function createUser(name: string, email?: string): object {
  return {
    name,
    email: email || "no-email@example.com"
  };
}

createUser("John"); // OK
createUser("John", "john@example.com"); // OK

// Default parameter
function greet(name: string, greeting: string = "Hello"): string {
  return `${greeting}, ${name}!`;
}

greet("John"); // "Hello, John!"
greet("John", "Hi"); // "Hi, John!"

// Optional parameters must come after required ones
function example(required: string, optional?: string, defaultParam: number = 10) {
  // ...
}
```

---

## Interfaces

### 12. What is an interface in TypeScript, and how is it used?

**Answer:** An interface defines the shape or structure that an object must conform to. It specifies required and optional properties, methods, and their types. Interfaces are used for type checking and can be implemented by classes.

**Example:**

```typescript
// Basic interface
interface Person {
  firstName: string;
  lastName: string;
  age: number;
}

function greet(person: Person): string {
  return `Hello, ${person.firstName} ${person.lastName}`;
}

const user: Person = {
  firstName: "John",
  lastName: "Doe",
  age: 30
};

console.log(greet(user)); // "Hello, John Doe"

// Interface with optional properties
interface User {
  id: number;
  name: string;
  email?: string; // Optional
}

// Interface with readonly properties
interface Point {
  readonly x: number;
  readonly y: number;
}

const point: Point = { x: 10, y: 20 };
// point.x = 30; // Error: Cannot assign to 'x' because it is a read-only property
```

### 13. What are the differences between interfaces and type aliases?

**Answer:** Both can describe object shapes, but they have differences:

- **Interfaces**: Can be extended and merged, better for object shapes
- **Type Aliases**: More flexible, can represent unions, intersections, primitives, etc.

**Example:**

```typescript
// Interface - can be extended and merged
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// Interface merging (declaration merging)
interface Window {
  customProperty: string;
}
interface Window {
  anotherProperty: number;
}
// Window now has both properties

// Type alias - more flexible
type Status = "active" | "inactive" | "pending";
type ID = string | number;

// Type alias for object
type Person = {
  name: string;
  age: number;
};

// Type alias can represent unions, intersections, etc.
type StringOrNumber = string | number;
type Combined = Person & { email: string };
```

### 14. How do you define optional and readonly properties in interfaces?

**Answer:** Use `?` for optional properties and `readonly` keyword for readonly properties.

**Example:**

```typescript
interface User {
  id: number;
  name: string;
  email?: string; // Optional property
  readonly createdAt: Date; // Readonly property
}

const user: User = {
  id: 1,
  name: "John",
  createdAt: new Date()
};

// user.createdAt = new Date(); // Error: Cannot assign to 'readonly' property
// user.email is optional, so it can be omitted

// Readonly array
interface Config {
  readonly settings: readonly string[];
}

const config: Config = {
  settings: ["setting1", "setting2"]
};

// config.settings.push("setting3"); // Error: Cannot add property
// config.settings[0] = "new"; // Error: Cannot assign to readonly
```

### 15. What are index signatures in interfaces?

**Answer:** Index signatures allow you to define the type of properties that are not explicitly listed in the interface.

**Example:**

```typescript
// String index signature
interface Dictionary {
  [key: string]: string;
}

const dict: Dictionary = {
  "key1": "value1",
  "key2": "value2"
};

// Number index signature
interface NumberDictionary {
  [index: number]: string;
}

const arr: NumberDictionary = ["first", "second"];

// Mixed index signatures
interface MixedDictionary {
  [key: string]: string | number;
  name: string; // Must match index signature type
  age: number; // Must match index signature type
}
```

---

## Classes

### 16. How do you define classes in TypeScript?

**Answer:** TypeScript classes are similar to JavaScript classes but with type annotations and access modifiers (`public`, `private`, `protected`).

**Example:**

```typescript
class Person {
  // Public properties (default)
  public name: string;
  public age: number;
  
  // Private property
  private ssn: string;
  
  // Protected property (accessible in subclasses)
  protected email: string;
  
  // Constructor
  constructor(name: string, age: number, ssn: string, email: string) {
    this.name = name;
    this.age = age;
    this.ssn = ssn;
    this.email = email;
  }
  
  // Public method
  public greet(): string {
    return `Hello, I'm ${this.name}`;
  }
  
  // Private method
  private getSSN(): string {
    return this.ssn;
  }
}

const person = new Person("John", 30, "123-45-6789", "john@example.com");
console.log(person.name); // OK
// console.log(person.ssn); // Error: Property 'ssn' is private
```

### 17. What are access modifiers in TypeScript classes?

**Answer:** TypeScript provides three access modifiers:

- **`public`**: Accessible everywhere (default)
- **`private`**: Only accessible within the class
- **`protected`**: Accessible within the class and its subclasses

**Example:**

```typescript
class Animal {
  public name: string; // Accessible everywhere
  private age: number; // Only accessible in this class
  protected species: string; // Accessible in this class and subclasses
  
  constructor(name: string, age: number, species: string) {
    this.name = name;
    this.age = age;
    this.species = species;
  }
  
  public getName(): string {
    return this.name;
  }
  
  private getAge(): number {
    return this.age; // Can access private property
  }
  
  protected getSpecies(): string {
    return this.species; // Can access protected property
  }
}

class Dog extends Animal {
  constructor(name: string, age: number) {
    super(name, age, "Canine");
  }
  
  public getInfo(): string {
    // Can access protected property
    return `${this.name} is a ${this.getSpecies()}`;
    // Cannot access private property: this.age
  }
}

const dog = new Dog("Buddy", 5);
console.log(dog.name); // OK - public
// console.log(dog.age); // Error - private
// console.log(dog.species); // Error - protected
```

### 18. What are abstract classes in TypeScript?

**Answer:** Abstract classes cannot be instantiated directly and must be extended. They can contain abstract methods that must be implemented by subclasses.

**Example:**

```typescript
// Abstract class
abstract class Animal {
  protected name: string;
  
  constructor(name: string) {
    this.name = name;
  }
  
  // Abstract method - must be implemented by subclasses
  abstract makeSound(): string;
  
  // Regular method
  public getName(): string {
    return this.name;
  }
}

// Concrete class extending abstract class
class Dog extends Animal {
  constructor(name: string) {
    super(name);
  }
  
  // Must implement abstract method
  makeSound(): string {
    return "Woof!";
  }
}

class Cat extends Animal {
  constructor(name: string) {
    super(name);
  }
  
  makeSound(): string {
    return "Meow!";
  }
}

// const animal = new Animal("Generic"); // Error: Cannot create instance of abstract class
const dog = new Dog("Buddy");
console.log(dog.makeSound()); // "Woof!"
```

### 19. How do you implement interfaces in classes?

**Answer:** Classes can implement interfaces using the `implements` keyword. A class must implement all required members of the interface.

**Example:**

```typescript
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

// Class implementing single interface
class Bird implements Flyable {
  fly(): void {
    console.log("Flying...");
  }
}

// Class implementing multiple interfaces
class Duck implements Flyable, Swimmable {
  fly(): void {
    console.log("Duck is flying");
  }
  
  swim(): void {
    console.log("Duck is swimming");
  }
}

// Class with properties from interface
interface Person {
  name: string;
  age: number;
  greet(): string;
}

class Employee implements Person {
  name: string;
  age: number;
  
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
  
  greet(): string {
    return `Hello, I'm ${this.name}`;
  }
}
```

### 20. What are getters and setters in TypeScript classes?

**Answer:** Getters and setters allow you to control access to class properties with custom logic.

**Example:**

```typescript
class Temperature {
  private _celsius: number = 0;
  
  // Getter
  get celsius(): number {
    return this._celsius;
  }
  
  // Setter
  set celsius(value: number) {
    if (value < -273.15) {
      throw new Error("Temperature cannot be below absolute zero");
    }
    this._celsius = value;
  }
  
  // Getter for computed property
  get fahrenheit(): number {
    return (this._celsius * 9/5) + 32;
  }
  
  set fahrenheit(value: number) {
    this._celsius = (value - 32) * 5/9;
  }
}

const temp = new Temperature();
temp.celsius = 25;
console.log(temp.celsius); // 25
console.log(temp.fahrenheit); // 77

temp.fahrenheit = 100;
console.log(temp.celsius); // 37.777...
```

---

## Enums

### 21. What are enums in TypeScript, and how are they used?

**Answer:** Enums allow you to define a set of named constants. They make code more readable and maintainable.

**Example:**

```typescript
// Numeric enum (default)
enum Direction {
  Up,    // 0
  Down,  // 1
  Left,  // 2
  Right  // 3
}

// Numeric enum with custom values
enum Status {
  Pending = 1,
  Approved = 2,
  Rejected = 3
}

// String enum
enum Color {
  Red = "RED",
  Green = "GREEN",
  Blue = "BLUE"
}

// Usage
let move: Direction = Direction.Up;
console.log(move); // 0
console.log(Direction[0]); // "Up"

let status: Status = Status.Approved;
let color: Color = Color.Red;
```

### 22. What are the different types of enums in TypeScript?

**Answer:** TypeScript supports three types of enums:

1. **Numeric Enums**: Default, auto-incremented numbers
2. **String Enums**: String values
3. **Heterogeneous Enums**: Mix of numbers and strings (not recommended)

**Example:**

```typescript
// Numeric enum
enum NumericEnum {
  First,   // 0
  Second, // 1
  Third   // 2
}

// Numeric enum with initial value
enum NumericEnum2 {
  First = 10,
  Second,  // 11
  Third    // 12
}

// String enum
enum StringEnum {
  North = "NORTH",
  South = "SOUTH",
  East = "EAST",
  West = "WEST"
}

// Heterogeneous enum (not recommended)
enum MixedEnum {
  No = 0,
  Yes = "YES"
}

// Const enum (inlined at compile time)
const enum ConstEnum {
  A = 1,
  B = 2
}
```

---

## Generics

### 23. What are generics in TypeScript, and why are they useful?

**Answer:** Generics allow you to create reusable components that work with multiple types while maintaining type safety. They enable writing flexible, type-safe code without using `any`.

**Example:**

```typescript
// Generic function
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("hello"); // Type is string
let output2 = identity<number>(42); // Type is number
let output3 = identity("world"); // Type inference: string

// Generic interface
interface Container<T> {
  value: T;
}

const stringContainer: Container<string> = { value: "hello" };
const numberContainer: Container<number> = { value: 42 };

// Generic class
class Box<T> {
  private content: T;
  
  constructor(content: T) {
    this.content = content;
  }
  
  getContent(): T {
    return this.content;
  }
}

const stringBox = new Box<string>("Hello");
const numberBox = new Box<number>(100);
```

### 24. How do you use multiple type parameters in generics?

**Answer:** You can define multiple type parameters separated by commas.

**Example:**

```typescript
// Multiple type parameters
function pair<T, U>(first: T, second: U): [T, U] {
  return [first, second];
}

const result = pair<string, number>("hello", 42);
// result is of type [string, number]

// Generic interface with multiple types
interface KeyValuePair<K, V> {
  key: K;
  value: V;
}

const pair1: KeyValuePair<string, number> = { key: "age", value: 30 };
const pair2: KeyValuePair<number, boolean> = { key: 1, value: true };

// Generic class with multiple types
class Map<K, V> {
  private items: Array<{ key: K; value: V }> = [];
  
  set(key: K, value: V): void {
    this.items.push({ key, value });
  }
  
  get(key: K): V | undefined {
    const item = this.items.find(i => i.key === key);
    return item ? item.value : undefined;
  }
}
```

### 25. What are generic constraints in TypeScript?

**Answer:** Generic constraints allow you to restrict the types that can be used with generics using the `extends` keyword.

**Example:**

```typescript
// Constraint: T must have a length property
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength("hello"); // OK - string has length
logLength([1, 2, 3]); // OK - array has length
// logLength(42); // Error - number doesn't have length

// Using keyof constraint
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person = { name: "John", age: 30 };
const name = getProperty(person, "name"); // OK
// const invalid = getProperty(person, "email"); // Error

// Constraint with multiple types
function merge<T extends object, U extends object>(obj1: T, obj2: U): T & U {
  return { ...obj1, ...obj2 };
}

const merged = merge({ name: "John" }, { age: 30 });
```

---

## Type Inference

### 26. What is type inference in TypeScript?

**Answer:** Type inference is TypeScript's ability to automatically determine the type of a variable based on its value, eliminating the need for explicit type annotations in many cases.

**Example:**

```typescript
// Type inference
let message = "Hello"; // TypeScript infers: string
let count = 42; // TypeScript infers: number
let isActive = true; // TypeScript infers: boolean

// Array inference
let numbers = [1, 2, 3]; // TypeScript infers: number[]
let mixed = [1, "hello", true]; // TypeScript infers: (string | number | boolean)[]

// Function return type inference
function add(a: number, b: number) {
  return a + b; // Return type inferred as number
}

// Object inference
const user = {
  name: "John",
  age: 30
}; // TypeScript infers: { name: string; age: number }

// Best common type inference
let arr = [0, 1, null]; // TypeScript infers: (number | null)[]
```

### 27. When should you use explicit type annotations vs. type inference?

**Answer:** Use explicit annotations when:
- Type cannot be inferred (function parameters, return types in some cases)
- You want to be explicit for documentation
- Inference gives `any` or too broad a type
- Public API boundaries

Use inference when:
- Type is obvious from initialization
- Reduces code verbosity
- Type is complex but correctly inferred

**Example:**

```typescript
// Explicit annotation - function parameters need types
function process(data: string, count: number): string {
  return data.repeat(count);
}

// Inference is fine for simple cases
let name = "John"; // Inference OK

// Explicit when inference is too broad
let data: string[] = []; // Explicit: empty array, inference would be any[]
// vs
let data2 = ["hello"]; // Inference OK: string[]

// Explicit for public APIs
export interface User {
  id: number;
  name: string;
}

export function createUser(id: number, name: string): User {
  return { id, name };
}
```

---

## Type Assertions

### 28. What is a type assertion in TypeScript?

**Answer:** Type assertions tell TypeScript to treat a value as a specific type. They don't perform runtime checks, only compile-time type checking. Use `as` syntax or angle bracket syntax.

**Example:**

```typescript
// Type assertion with 'as'
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;

// Type assertion with angle brackets (not in JSX)
let anotherValue: any = "hello";
let strLength2: number = (<string>anotherValue).length;

// Asserting to more specific type
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

let animal: Animal = { name: "Buddy" };
let dog = animal as Dog; // Assertion, but dog.breed would be undefined at runtime

// Double assertion
let value: unknown = "hello";
let str = value as unknown as string; // Double assertion through unknown
```

### 29. What is the difference between type assertions and type guards?

**Answer:** Type assertions tell the compiler to treat a value as a type (no runtime check). Type guards are runtime checks that narrow types.

**Example:**

```typescript
// Type assertion - no runtime check
function processValue(value: unknown) {
  let str = value as string; // Asserts, but no check
  console.log(str.toUpperCase()); // Might fail at runtime if value isn't string
}

// Type guard - runtime check
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function processValueSafe(value: unknown) {
  if (isString(value)) {
    // TypeScript knows value is string here
    console.log(value.toUpperCase()); // Safe
  }
}

// Built-in type guards
function example(x: string | number) {
  if (typeof x === "string") {
    // x is string here
    console.log(x.length);
  } else {
    // x is number here
    console.log(x.toFixed(2));
  }
}
```

---

## Union and Intersection Types

### 30. What are union types in TypeScript?

**Answer:** Union types allow a value to be one of several types, defined using the `|` operator.

**Example:**

```typescript
// Union type
function printId(id: number | string) {
  console.log(`ID: ${id}`);
}

printId(101); // OK
printId("202"); // OK
// printId(true); // Error

// Union with multiple types
type Status = "pending" | "approved" | "rejected";

function handleStatus(status: Status) {
  switch (status) {
    case "pending":
      return "Processing...";
    case "approved":
      return "Done!";
    case "rejected":
      return "Failed";
  }
}

// Union in arrays
let mixedArray: (string | number)[] = ["hello", 42, "world", 100];

// Union with null/undefined
type MaybeString = string | null | undefined;
```

### 31. What are intersection types in TypeScript?

**Answer:** Intersection types combine multiple types into one, defined using the `&` operator. A value must satisfy all types in the intersection.

**Example:**

```typescript
// Intersection type
interface Flyable {
  fly(): void;
}

interface Swimmable {
  swim(): void;
}

type Duck = Flyable & Swimmable;

const duck: Duck = {
  fly() {
    console.log("Flying");
  },
  swim() {
    console.log("Swimming");
  }
};

// Intersection of object types
type Person = {
  name: string;
  age: number;
};

type Employee = {
  employeeId: number;
  department: string;
};

type EmployeePerson = Person & Employee;

const emp: EmployeePerson = {
  name: "John",
  age: 30,
  employeeId: 123,
  department: "IT"
};

// Intersection with primitives (results in never)
type Impossible = string & number; // never
```

---

## Type Aliases

### 32. What are type aliases in TypeScript?

**Answer:** Type aliases create a new name for a type. They can represent primitives, unions, intersections, tuples, and more.

**Example:**

```typescript
// Type alias for primitive
type ID = string | number;

// Type alias for object
type User = {
  id: ID;
  name: string;
  email: string;
};

// Type alias for union
type Status = "active" | "inactive" | "pending";

// Type alias for function
type MathOperation = (a: number, b: number) => number;

const add: MathOperation = (a, b) => a + b;
const multiply: MathOperation = (a, b) => a * b;

// Type alias for tuple
type Point = [number, number];

// Generic type alias
type Container<T> = {
  value: T;
};

// Recursive type alias
type TreeNode = {
  value: number;
  left?: TreeNode;
  right?: TreeNode;
};
```

### 33. What is the difference between type aliases and interfaces?

**Answer:** Key differences:

- **Interfaces**: Can be merged (declaration merging), extended with `extends`, better for object shapes
- **Type Aliases**: More flexible, can represent unions, intersections, primitives, tuples, cannot be merged

**Example:**

```typescript
// Interface - can be merged
interface User {
  name: string;
}
interface User {
  age: number;
}
// User now has both name and age

// Interface - can be extended
interface Person extends User {
  email: string;
}

// Type alias - cannot be merged
type UserType = {
  name: string;
};
// Cannot redeclare UserType

// Type alias - more flexible
type ID = string | number; // Union
type Status = "active" | "inactive"; // Union of literals
type Point = [number, number]; // Tuple

// Both can describe objects
interface Animal {
  name: string;
}

type AnimalType = {
  name: string;
};

// Choose interface for object shapes that might be extended
// Choose type alias for unions, intersections, primitives, etc.
```

---

## Modules and Namespaces

### 34. How do you export and import modules in TypeScript?

**Answer:** TypeScript uses ES6 module syntax with `export` and `import` keywords.

**Example:**

```typescript
// math.ts - Named exports
export function add(a: number, b: number): number {
  return a + b;
}

export function subtract(a: number, b: number): number {
  return a - b;
}

export const PI = 3.14159;

// Default export
export default function multiply(a: number, b: number): number {
  return a * b;
}

// main.ts - Imports
import multiply, { add, subtract, PI } from './math';

// Or import all as namespace
import * as Math from './math';
console.log(Math.add(2, 3));

// Re-exporting
export { add, subtract } from './math';

// Type exports
export type { User } from './types';
```

### 35. What are namespaces in TypeScript?

**Answer:** Namespaces are a way to organize code and avoid naming conflicts. They create a scope for variables, functions, classes, etc.

**Example:**

```typescript
// Namespace declaration
namespace Geometry {
  export interface Point {
    x: number;
    y: number;
  }
  
  export class Circle {
    constructor(public radius: number) {}
    
    area(): number {
      return Math.PI * this.radius ** 2;
    }
  }
  
  export function distance(p1: Point, p2: Point): number {
    return Math.sqrt((p2.x - p1.x) ** 2 + (p2.y - p1.y) ** 2);
  }
}

// Usage
const circle = new Geometry.Circle(5);
const point1: Geometry.Point = { x: 0, y: 0 };
const point2: Geometry.Point = { x: 3, y: 4 };

// Nested namespaces
namespace Geometry {
  export namespace Shapes {
    export class Rectangle {
      constructor(public width: number, public height: number) {}
      
      area(): number {
        return this.width * this.height;
      }
    }
  }
}

const rect = new Geometry.Shapes.Rectangle(10, 20);
```

---

## Advanced Types

### 36. What are mapped types in TypeScript?

**Answer:** Mapped types create new types by transforming properties of an existing type. They use the `in` keyword to iterate over keys.

**Example:**

```typescript
// Basic mapped type
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

interface Person {
  name: string;
  age: number;
}

type ReadonlyPerson = Readonly<Person>;
// { readonly name: string; readonly age: number; }

// Partial mapped type
type Partial<T> = {
  [P in keyof T]?: T[P];
};

type PartialPerson = Partial<Person>;
// { name?: string; age?: number; }

// Custom mapped type
type Optional<T> = {
  [P in keyof T]?: T[P] | null;
};

// Mapped type with modifiers
type Required<T> = {
  [P in keyof T]-?: T[P]; // Remove optional modifier
};

// Mapped type with key remapping
type Getters<T> = {
  [P in keyof T as `get${Capitalize<string & P>}`]: () => T[P];
};
```

### 37. What are conditional types in TypeScript?

**Answer:** Conditional types select one of two types based on a condition, similar to a ternary operator but for types.

**Example:**

```typescript
// Basic conditional type
type IsArray<T> = T extends Array<any> ? true : false;

type Test1 = IsArray<string[]>; // true
type Test2 = IsArray<string>; // false

// Extract array element type
type ArrayElement<T> = T extends Array<infer U> ? U : never;

type Element = ArrayElement<string[]>; // string
type Element2 = ArrayElement<number[]>; // number

// NonNullable utility type
type NonNullable<T> = T extends null | undefined ? never : T;

type Test3 = NonNullable<string | null>; // string
type Test4 = NonNullable<number | undefined>; // number

// Function return type extraction
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

type FuncReturn = ReturnType<() => string>; // string

// Distributive conditional types
type ToArray<T> = T extends any ? T[] : never;

type StrArrOrNumArr = ToArray<string | number>; // string[] | number[]
```

### 38. What are template literal types in TypeScript?

**Answer:** Template literal types allow you to create string literal types using template string syntax, enabling pattern matching on string types.

**Example:**

```typescript
// Basic template literal type
type Greeting = `Hello, ${string}`;

const greet: Greeting = "Hello, World"; // OK
// const invalid: Greeting = "Hi"; // Error

// With union types
type EventName<T extends string> = `on${Capitalize<T>}`;

type ClickEvent = EventName<"click">; // "onClick"
type ChangeEvent = EventName<"change">; // "onChange"

// Complex template literal types
type PropertyPath<T> = {
  [K in keyof T]: K extends string
    ? T[K] extends object
      ? `${K}.${PropertyPath<T[K]>}`
      : K
    : never;
}[keyof T];

// API endpoint types
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";
type ApiEndpoint = `/${string}`;

type ApiRoute = `${HttpMethod} ${ApiEndpoint}`;

const route: ApiRoute = "GET /users"; // OK
// const invalid: ApiRoute = "PATCH /users"; // Error
```

---

## Utility Types

### 39. What are utility types in TypeScript? List the most common ones.

**Answer:** Utility types are built-in generic types that facilitate common type transformations. Common ones include:

- `Partial<T>`: Makes all properties optional
- `Required<T>`: Makes all properties required
- `Readonly<T>`: Makes all properties readonly
- `Pick<T, K>`: Selects specific properties
- `Omit<T, K>`: Removes specific properties
- `Record<K, T>`: Creates object type with keys K and values T
- `Exclude<T, U>`: Excludes types from union
- `Extract<T, U>`: Extracts types from union
- `NonNullable<T>`: Removes null and undefined
- `ReturnType<T>`: Gets function return type
- `Parameters<T>`: Gets function parameters as tuple

**Example:**

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age: number;
}

// Partial - all properties optional
type PartialUser = Partial<User>;
const partial: PartialUser = { name: "John" }; // OK

// Required - all properties required
type RequiredUser = Required<PartialUser>;

// Readonly - all properties readonly
type ReadonlyUser = Readonly<User>;

// Pick - select specific properties
type UserPreview = Pick<User, "id" | "name">;
const preview: UserPreview = { id: 1, name: "John" };

// Omit - remove specific properties
type UserWithoutEmail = Omit<User, "email">;

// Record - create object type
type UserMap = Record<string, User>;
const users: UserMap = {
  "user1": { id: 1, name: "John", email: "john@example.com", age: 30 }
};

// Exclude - exclude from union
type T0 = Exclude<"a" | "b" | "c", "a">; // "b" | "c"

// Extract - extract from union
type T1 = Extract<"a" | "b" | "c", "a" | "f">; // "a"

// ReturnType
function getUser(): User {
  return { id: 1, name: "John", email: "john@example.com", age: 30 };
}
type UserReturn = ReturnType<typeof getUser>; // User

// Parameters
function createUser(id: number, name: string): User {
  return { id, name, email: "", age: 0 };
}
type CreateUserParams = Parameters<typeof createUser>; // [number, string]
```

---

## Type Guards

### 40. What are type guards in TypeScript?

**Answer:** Type guards are expressions that perform runtime checks to narrow types. They help TypeScript understand the type of a value in a specific scope.

**Example:**

```typescript
// typeof type guard
function process(value: string | number) {
  if (typeof value === "string") {
    // TypeScript knows value is string here
    console.log(value.toUpperCase());
  } else {
    // TypeScript knows value is number here
    console.log(value.toFixed(2));
  }
}

// instanceof type guard
class Dog {
  bark() {
    console.log("Woof!");
  }
}

class Cat {
  meow() {
    console.log("Meow!");
  }
}

function makeSound(animal: Dog | Cat) {
  if (animal instanceof Dog) {
    animal.bark(); // TypeScript knows it's Dog
  } else {
    animal.meow(); // TypeScript knows it's Cat
  }
}

// Custom type guard function
interface Fish {
  swim(): void;
}

interface Bird {
  fly(): void;
}

function isFish(animal: Fish | Bird): animal is Fish {
  return (animal as Fish).swim !== undefined;
}

function move(animal: Fish | Bird) {
  if (isFish(animal)) {
    animal.swim(); // TypeScript knows it's Fish
  } else {
    animal.fly(); // TypeScript knows it's Bird
  }
}

// in operator type guard
interface Car {
  drive(): void;
}

interface Boat {
  sail(): void;
}

function operate(vehicle: Car | Boat) {
  if ("drive" in vehicle) {
    vehicle.drive(); // TypeScript knows it's Car
  } else {
    vehicle.sail(); // TypeScript knows it's Boat
  }
}
```

### 41. How do you create custom type guard functions?

**Answer:** Custom type guards are functions that return a type predicate (`parameterName is Type`) to narrow types.

**Example:**

```typescript
// Custom type guard
function isString(value: unknown): value is string {
  return typeof value === "string";
}

function isNumber(value: unknown): value is number {
  return typeof value === "number" && !isNaN(value);
}

function processValue(value: unknown) {
  if (isString(value)) {
    // TypeScript knows value is string
    console.log(value.length);
  } else if (isNumber(value)) {
    // TypeScript knows value is number
    console.log(value.toFixed(2));
  }
}

// Type guard for objects
interface Admin {
  role: "admin";
  permissions: string[];
}

interface User {
  role: "user";
  email: string;
}

function isAdmin(user: Admin | User): user is Admin {
  return user.role === "admin";
}

function checkAccess(user: Admin | User) {
  if (isAdmin(user)) {
    // TypeScript knows user is Admin
    console.log(user.permissions);
  } else {
    // TypeScript knows user is User
    console.log(user.email);
  }
}

// Type guard for arrays
function isStringArray(value: unknown): value is string[] {
  return Array.isArray(value) && value.every(item => typeof item === "string");
}
```

---

## Decorators

### 42. What are decorators in TypeScript?

**Answer:** Decorators are special declarations that can be attached to classes, methods, properties, or parameters. They use the `@` syntax and are experimental (require `experimentalDecorators` in tsconfig.json).

**Example:**

```typescript
// Class decorator
function sealed(constructor: Function) {
  Object.seal(constructor);
  Object.seal(constructor.prototype);
}

@sealed
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return `Hello, ${this.greeting}`;
  }
}

// Method decorator
function log(target: any, propertyName: string, descriptor: PropertyDescriptor) {
  const method = descriptor.value;
  
  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyName} with`, args);
    return method.apply(this, args);
  };
}

class Calculator {
  @log
  add(a: number, b: number): number {
    return a + b;
  }
}

// Property decorator
function readonly(target: any, propertyName: string) {
  Object.defineProperty(target, propertyName, {
    writable: false
  });
}

class Person {
  @readonly
  name: string = "John";
}

// Parameter decorator
function validate(target: any, propertyName: string, parameterIndex: number) {
  // Validation logic
}

class UserService {
  createUser(@validate name: string, @validate email: string) {
    // ...
  }
}
```

### 43. How do decorator factories work?

**Answer:** Decorator factories are functions that return decorator functions, allowing you to pass parameters to decorators.

**Example:**

```typescript
// Decorator factory
function log(prefix: string) {
  return function (target: any, propertyName: string, descriptor: PropertyDescriptor) {
    const method = descriptor.value;
    
    descriptor.value = function (...args: any[]) {
      console.log(`[${prefix}] Calling ${propertyName}`, args);
      const result = method.apply(this, args);
      console.log(`[${prefix}] Result:`, result);
      return result;
    };
  };
}

class Calculator {
  @log("CALC")
  add(a: number, b: number): number {
    return a + b;
  }
}

// Property decorator factory
function format(formatString: string) {
  return function (target: any, propertyName: string) {
    let value: string;
    
    const getter = function () {
      return value;
    };
    
    const setter = function (newVal: string) {
      value = formatString.replace("{value}", newVal);
    };
    
    Object.defineProperty(target, propertyName, {
      get: getter,
      set: setter
    });
  };
}

class Message {
  @format("Message: {value}")
  text: string = "";
}

const msg = new Message();
msg.text = "Hello";
console.log(msg.text); // "Message: Hello"
```

---

## Mixins

### 44. What are mixins in TypeScript, and how are they implemented?

**Answer:** Mixins are a pattern that allows classes to be composed from multiple reusable components, enabling multiple inheritance-like behavior.

**Example:**

```typescript
// Disposable mixin
class Disposable {
  isDisposed: boolean = false;
  dispose() {
    this.isDisposed = true;
  }
}

// Activatable mixin
class Activatable {
  isActive: boolean = false;
  activate() {
    this.isActive = true;
  }
  deactivate() {
    this.isActive = false;
  }
}

// Class that uses mixins
class SmartObject implements Disposable, Activatable {
  // Disposable
  isDisposed: boolean = false;
  dispose: () => void;
  
  // Activatable
  isActive: boolean = false;
  activate: () => void;
  deactivate: () => void;
  
  interact() {
    this.activate();
  }
}

// Mixin application function
function applyMixins(derivedCtor: any, baseCtors: any[]) {
  baseCtors.forEach(baseCtor => {
    Object.getOwnPropertyNames(baseCtor.prototype).forEach(name => {
      if (name !== "constructor") {
        derivedCtor.prototype[name] = baseCtor.prototype[name];
      }
    });
  });
}

applyMixins(SmartObject, [Disposable, Activatable]);

const smartObj = new SmartObject();
smartObj.activate();
smartObj.dispose();

// Alternative: Using intersection types and helper function
type Constructor<T = {}> = new (...args: any[]) => T;

function Timestamped<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    timestamp = Date.now();
  };
}

function Tagged<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    tag = "default";
  };
}

class User {
  name = "";
}

const TimestampedTaggedUser = Timestamped(Tagged(User));
const user = new TimestampedTaggedUser();
console.log(user.timestamp);
console.log(user.tag);
```

---

## Conditional Types

### 45. Explain conditional types with examples.

**Answer:** Conditional types select types based on conditions using the syntax `T extends U ? X : Y`.

**Example:**

```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type Test1 = IsString<string>; // true
type Test2 = IsString<number>; // false

// Extract array element type
type Flatten<T> = T extends Array<infer U> ? U : T;

type Str = Flatten<string[]>; // string
type Num = Flatten<number>; // number

// Function return type
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

type Func = () => string;
type Ret = ReturnType<Func>; // string

// Non-nullable type
type NonNullable<T> = T extends null | undefined ? never : T;

type Test3 = NonNullable<string | null>; // string
type Test4 = NonNullable<number | undefined>; // number

// Distributive conditional types
type ToArray<T> = T extends any ? T[] : never;

type StrArrOrNumArr = ToArray<string | number>; // string[] | number[]

// Prevent distribution with brackets
type ToArrayNonDist<T> = [T] extends [any] ? T[] : never;

type Arr = ToArrayNonDist<string | number>; // (string | number)[]

// Extract function parameters
type Parameters<T> = T extends (...args: infer P) => any ? P : never;

type FuncParams = Parameters<(a: string, b: number) => void>; // [string, number]
```

---

## Mapped Types

### 46. Explain mapped types with practical examples.

**Answer:** Mapped types create new types by transforming properties of existing types using the `in` keyword.

**Example:**

```typescript
// Basic mapped type
type Readonly<T> = {
  readonly [P in keyof T]: T[P];
};

interface Person {
  name: string;
  age: number;
}

type ReadonlyPerson = Readonly<Person>;
// { readonly name: string; readonly age: number; }

// Partial type
type Partial<T> = {
  [P in keyof T]?: T[P];
};

// Required type (remove optional)
type Required<T> = {
  [P in keyof T]-?: T[P];
};

// Pick type
type Pick<T, K extends keyof T> = {
  [P in K]: T[P];
};

// Omit type (using Exclude)
type Omit<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

// Custom mapped type - make all properties nullable
type Nullable<T> = {
  [P in keyof T]: T[P] | null;
};

// Mapped type with key remapping (TypeScript 4.1+)
type Getters<T> = {
  [P in keyof T as `get${Capitalize<string & P>}`]: () => T[P];
};

interface User {
  name: string;
  age: number;
}

type UserGetters = Getters<User>;
// { getName: () => string; getAge: () => number; }

// Filter out properties
type NonFunctionPropertyNames<T> = {
  [K in keyof T]: T[K] extends Function ? never : K;
}[keyof T];

type NonFunctionProperties<T> = Pick<T, NonFunctionPropertyNames<T>>;
```

---

## Template Literal Types

### 47. What are template literal types, and how are they used?

**Answer:** Template literal types create string literal types using template string syntax, enabling pattern matching and string manipulation at the type level.

**Example:**

```typescript
// Basic template literal type
type World = "world";
type Greeting = `hello ${World}`; // "hello world"

// With union types
type Color = "red" | "blue" | "green";
type Size = "small" | "medium" | "large";

type ColoredSize = `${Color}-${Size}`;
// "red-small" | "red-medium" | "red-large" | "blue-small" | ...

// Event handler types
type EventName<T extends string> = `on${Capitalize<T>}`;

type ClickEvent = EventName<"click">; // "onClick"
type ChangeEvent = EventName<"change">; // "onChange"

// API route types
type HttpMethod = "GET" | "POST" | "PUT" | "DELETE";
type ApiEndpoint = `/${string}`;

type ApiRoute = `${HttpMethod} ${ApiEndpoint}`;

const route1: ApiRoute = "GET /users"; // OK
const route2: ApiRoute = "POST /api/login"; // OK
// const route3: ApiRoute = "PATCH /users"; // Error

// Property path types
type PropPath<T> = {
  [K in keyof T]: K extends string
    ? T[K] extends object
      ? `${K}.${PropPath<T[K]>}`
      : K
    : never;
}[keyof T];

interface User {
  name: string;
  address: {
    street: string;
    city: string;
  };
}

type UserPath = PropPath<User>; // "name" | "address.street" | "address.city"

// String manipulation utilities
type Uppercase<S extends string> = intrinsic;
type Lowercase<S extends string> = intrinsic;
type Capitalize<S extends string> = intrinsic;
type Uncapitalize<S extends string> = intrinsic;
```

---

## TypeScript Configuration

### 48. What are the important compiler options in tsconfig.json?

**Answer:** Key compiler options include:

- `target`: ECMAScript version to compile to
- `module`: Module system to use
- `strict`: Enable all strict type checking
- `esModuleInterop`: Enable interoperability with CommonJS
- `skipLibCheck`: Skip type checking of declaration files
- `outDir`: Output directory for compiled files
- `rootDir`: Root directory of input files

**Example:**

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020", "DOM"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

### 49. What is the difference between `interface` and `type` when extending?

**Answer:** Both can extend, but with different syntax and capabilities.

**Example:**

```typescript
// Interface extends interface
interface Animal {
  name: string;
}

interface Dog extends Animal {
  breed: string;
}

// Interface extends type alias
type AnimalType = {
  name: string;
};

interface Cat extends AnimalType {
  meow: boolean;
}

// Type alias extends interface (using intersection)
interface Bird {
  fly: boolean;
}

type Parrot = Bird & {
  talk: boolean;
};

// Type alias extends type alias (using intersection)
type Fish = {
  swim: boolean;
};

type Shark = Fish & {
  dangerous: boolean;
};

// Interface can extend multiple
interface Duck extends Animal, Bird {
  swim: boolean;
}

// Type alias can intersect multiple
type Platypus = Animal & Bird & {
  layEggs: boolean;
};
```

---

## Error Handling

### 50. How do you handle errors in TypeScript?

**Answer:** TypeScript doesn't have built-in exception types, but you can create custom error types and use try-catch blocks.

**Example:**

```typescript
// Custom error class
class ValidationError extends Error {
  constructor(message: string, public field: string) {
    super(message);
    this.name = "ValidationError";
  }
}

class NotFoundError extends Error {
  constructor(message: string) {
    super(message);
    this.name = "NotFoundError";
  }
}

// Error handling
function validateUser(user: { name?: string; email?: string }) {
  if (!user.name) {
    throw new ValidationError("Name is required", "name");
  }
  if (!user.email) {
    throw new ValidationError("Email is required", "email");
  }
}

function getUser(id: number) {
  if (id < 0) {
    throw new NotFoundError(`User with id ${id} not found`);
  }
  return { id, name: "John", email: "john@example.com" };
}

// Try-catch with type guards
try {
  validateUser({});
  const user = getUser(1);
} catch (error) {
  if (error instanceof ValidationError) {
    console.error(`Validation error in ${error.field}: ${error.message}`);
  } else if (error instanceof NotFoundError) {
    console.error(`Not found: ${error.message}`);
  } else {
    console.error("Unknown error:", error);
  }
}

// Result type pattern (alternative to exceptions)
type Result<T, E = Error> = 
  | { success: true; data: T }
  | { success: false; error: E };

function divide(a: number, b: number): Result<number, string> {
  if (b === 0) {
    return { success: false, error: "Division by zero" };
  }
  return { success: true, data: a / b };
}

const result = divide(10, 2);
if (result.success) {
  console.log(result.data); // TypeScript knows data exists
} else {
  console.error(result.error); // TypeScript knows error exists
}
```

---

## Best Practices

### 51. What are TypeScript best practices?

**Answer:** Key best practices include:

1. **Use strict mode**: Enable `strict` in tsconfig.json
2. **Avoid `any`**: Use `unknown` when type is truly unknown
3. **Prefer interfaces for object shapes**: Use type aliases for unions, intersections
4. **Use const assertions**: For literal types
5. **Leverage type inference**: Don't over-annotate
6. **Use utility types**: Don't reinvent the wheel
7. **Enable noImplicitAny**: Catch implicit any types
8. **Use readonly**: For immutable data
9. **Prefer union types over enums**: For string literals
10. **Use type guards**: For runtime type checking

**Example:**

```typescript
// ✅ Good: Use const assertion
const colors = ["red", "green", "blue"] as const;
type Color = typeof colors[number]; // "red" | "green" | "blue"

// ❌ Bad: Using any
function process(data: any) {
  return data.something;
}

// ✅ Good: Use unknown with type guard
function process(data: unknown) {
  if (typeof data === "object" && data !== null && "something" in data) {
    return (data as { something: string }).something;
  }
}

// ✅ Good: Use readonly
interface Config {
  readonly apiUrl: string;
  readonly timeout: number;
}

// ✅ Good: Use utility types
type PartialUser = Partial<User>;
type UserEmail = Pick<User, "email">;

// ✅ Good: Type guards
function isString(value: unknown): value is string {
  return typeof value === "string";
}

// ✅ Good: Prefer union over enum for string literals
type Status = "pending" | "approved" | "rejected";
// Instead of: enum Status { Pending, Approved, Rejected }
```

### 52. How do you structure TypeScript projects?

**Answer:** Best practices for project structure:

**Example:**

```
src/
  types/
    index.ts          # Type definitions
    user.ts
    api.ts
  interfaces/
    index.ts          # Interface definitions
  classes/
    User.ts
    Service.ts
  utils/
    helpers.ts
    validators.ts
  services/
    api.service.ts
  components/         # If using a framework
  app.ts
  index.ts
tsconfig.json
package.json
```

```typescript
// types/user.ts
export type UserId = string | number;
export type UserRole = "admin" | "user" | "guest";

// interfaces/user.ts
export interface User {
  id: UserId;
  name: string;
  role: UserRole;
}

// services/user.service.ts
import { User, UserId } from '../types';

export class UserService {
  getUser(id: UserId): Promise<User> {
    // Implementation
  }
}

// Use barrel exports
// types/index.ts
export * from './user';
export * from './api';
```

---

## Additional Advanced Topics

### 53. What are branded types in TypeScript?

**Answer:** Branded types create distinct types from primitives to prevent mixing them up, even if they have the same underlying type.

**Example:**

```typescript
// Branded type
type UserId = string & { readonly brand: unique symbol };
type ProductId = string & { readonly brand: unique symbol };

function createUserId(id: string): UserId {
  return id as UserId;
}

function createProductId(id: string): ProductId {
  return id as ProductId;
}

const userId = createUserId("user-123");
const productId = createProductId("user-123");

function getUser(id: UserId) {
  // Implementation
}

getUser(userId); // OK
// getUser(productId); // Error: Type 'ProductId' is not assignable to type 'UserId'

// Alternative: Using nominal typing
declare const __brand: unique symbol;
type Brand<T, TBrand> = T & { [__brand]: TBrand };

type BrandedUserId = Brand<string, "UserId">;
type BrandedProductId = Brand<string, "ProductId">;
```

### 54. What are recursive types in TypeScript?

**Answer:** Recursive types are types that reference themselves, useful for tree structures, linked lists, etc.

**Example:**

```typescript
// Recursive type for tree
type TreeNode = {
  value: number;
  left?: TreeNode;
  right?: TreeNode;
};

// Recursive type for linked list
type ListNode<T> = {
  value: T;
  next?: ListNode<T>;
};

// Recursive type alias
type JsonValue = 
  | string
  | number
  | boolean
  | null
  | JsonValue[]
  | { [key: string]: JsonValue };

// Recursive interface
interface FileSystemNode {
  name: string;
  type: "file" | "directory";
  children?: FileSystemNode[];
}

// Usage
const tree: TreeNode = {
  value: 1,
  left: {
    value: 2,
    left: { value: 4 },
    right: { value: 5 }
  },
  right: {
    value: 3
  }
};
```

### 55. How do you work with async/await in TypeScript?

**Answer:** TypeScript fully supports async/await with proper typing for Promises.

**Example:**

```typescript
// Async function return type
async function fetchUser(id: number): Promise<User> {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}

// Async function with error handling
async function fetchUserSafe(id: number): Promise<User | null> {
  try {
    const response = await fetch(`/api/users/${id}`);
    if (!response.ok) {
      return null;
    }
    return await response.json();
  } catch (error) {
    console.error("Error fetching user:", error);
    return null;
  }
}

// Promise type
type ApiResponse<T> = Promise<{
  data: T;
  status: number;
}>;

async function getData(): ApiResponse<User[]> {
  const response = await fetch("/api/users");
  return {
    data: await response.json(),
    status: response.status
  };
}

// Parallel async operations
async function fetchMultipleUsers(ids: number[]): Promise<User[]> {
  const promises = ids.map(id => fetchUser(id));
  return Promise.all(promises);
}

// Async generator
async function* asyncGenerator(): AsyncGenerator<number> {
  for (let i = 0; i < 5; i++) {
    await new Promise(resolve => setTimeout(resolve, 1000));
    yield i;
  }
}

// Using async generator
async function consume() {
  for await (const value of asyncGenerator()) {
    console.log(value);
  }
}
```

---

## Summary

This comprehensive guide covers all major TypeScript topics from the roadmap, including:

- **Fundamentals**: Types, variables, functions, interfaces, classes
- **Advanced Types**: Generics, unions, intersections, conditional types, mapped types
- **Language Features**: Enums, modules, namespaces, decorators, mixins
- **Type System**: Type inference, type guards, type assertions, utility types
- **Modern Features**: Template literal types, branded types, recursive types
- **Best Practices**: Project structure, error handling, configuration

Each topic includes detailed explanations, practical examples, and interview-style questions to help you master TypeScript for interviews and real-world development.

---

*Based on the TypeScript Developer Roadmap from [roadmap.sh/typescript](https://roadmap.sh/typescript)*

