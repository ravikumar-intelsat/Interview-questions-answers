# C# Interview Questions and Answers

## Table of Contents
1. [C# Basics and Fundamentals](#c-basics-and-fundamentals)
2. [Object-Oriented Programming (OOP)](#object-oriented-programming-oop)
3. [Collections and Generics](#collections-and-generics)
4. [LINQ](#linq)
5. [Async/Await and Asynchronous Programming](#asyncawait-and-asynchronous-programming)
6. [Exception Handling](#exception-handling)
7. [Memory Management and Garbage Collection](#memory-management-and-garbage-collection)
8. [Delegates and Events](#delegates-and-events)
9. [Reflection](#reflection)
10. [Attributes](#attributes)
11. [Threading and Concurrency](#threading-and-concurrency)
12. [Design Patterns](#design-patterns)
13. [Entity Framework](#entity-framework)
14. [ASP.NET Core](#aspnet-core)
15. [Advanced Topics](#advanced-topics)

---

## C# Basics and Fundamentals

### Q1: What is C# and what are its key features?
**Answer:**
C# is a modern, object-oriented programming language developed by Microsoft. Key features include:
- **Type-safe**: Strongly typed language with compile-time type checking
- **Object-oriented**: Supports encapsulation, inheritance, polymorphism, and abstraction
- **Component-oriented**: Supports properties, events, and attributes
- **Garbage Collection**: Automatic memory management
- **Cross-platform**: Runs on .NET Core/.NET 5+ on Windows, Linux, and macOS
- **Rich Standard Library**: Extensive .NET Framework/Core libraries
- **Language Integrated Query (LINQ)**: Query capabilities integrated into the language
- **Async/Await**: Built-in support for asynchronous programming

### Q2: What is the difference between value types and reference types?
**Answer:**
- **Value Types**: Stored on the stack, directly contain their data
  - Examples: `int`, `bool`, `char`, `struct`, `enum`
  - When assigned, a copy is created
  - Default value is zero/null for the type
  
- **Reference Types**: Stored on the heap, contain a reference to the data
  - Examples: `class`, `interface`, `delegate`, `string`, `array`
  - When assigned, the reference is copied (both point to same object)
  - Default value is `null`

```csharp
// Value type example
int a = 10;
int b = a;  // b is a copy of a
b = 20;     // a is still 10

// Reference type example
MyClass obj1 = new MyClass();
MyClass obj2 = obj1;  // obj2 references the same object
obj2.Value = 20;      // obj1.Value is also 20
```

### Q3: Explain the difference between `const`, `readonly`, and `static readonly`.
**Answer:**
- **`const`**: 
  - Compile-time constant, must be initialized at declaration
  - Value must be known at compile time
  - Cannot be changed after compilation
  - Implicitly `static`
  
- **`readonly`**: 
  - Runtime constant, can be initialized at declaration or in constructor
  - Can be instance or static
  - Cannot be modified after initialization
  
- **`static readonly`**: 
  - Similar to `readonly` but shared across all instances
  - Can be initialized at declaration or in static constructor

```csharp
public class Example
{
    public const int ConstValue = 10;           // Compile-time constant
    public readonly int ReadOnlyValue = 20;     // Instance readonly
    public static readonly int StaticReadOnly = 30; // Static readonly
    
    public Example(int value)
    {
        ReadOnlyValue = value;  // Can be set in constructor
        // ConstValue = 50;     // Error: cannot modify const
    }
}
```

### Q4: What is the difference between `string` and `StringBuilder`?
**Answer:**
- **`string`**: 
  - Immutable - once created, cannot be changed
  - Operations like concatenation create new string objects
  - Good for small, infrequent string operations
  
- **`StringBuilder`**: 
  - Mutable - can be modified without creating new objects
  - More efficient for multiple string operations
  - Better memory management for large string manipulations

```csharp
// String - creates new objects
string str = "Hello";
str += " World";  // Creates new string object

// StringBuilder - modifies existing object
StringBuilder sb = new StringBuilder("Hello");
sb.Append(" World");  // Modifies existing object
string result = sb.ToString();
```

### Q5: What are nullable value types in C#?
**Answer:**
Nullable value types allow value types to have `null` values. Use `?` syntax or `Nullable<T>`.

```csharp
int? nullableInt = null;  // or Nullable<int>
bool? nullableBool = true;
nullableInt = 10;

// Checking for null
if (nullableInt.HasValue)
{
    int value = nullableInt.Value;  // or nullableInt ?? 0
}

// Null coalescing operator
int result = nullableInt ?? 0;  // Returns 0 if null
```

### Q6: Explain the `var` keyword and when to use it.
**Answer:**
`var` is used for implicit type declaration. The compiler infers the type from the initialization.

```csharp
var number = 10;        // int
var name = "John";      // string
var list = new List<int>();  // List<int>

// Use var when:
// 1. Type is obvious from right side
var dictionary = new Dictionary<string, int>();

// 2. Anonymous types (required)
var anonymous = new { Name = "John", Age = 30 };

// Don't use var when:
// 1. Type is not clear
var data = GetData();  // What type is data?

// 2. Primitive types (optional, but explicit is clearer)
int count = 10;  // Better than var count = 10;
```

---

## Object-Oriented Programming (OOP)

### Q7: Explain the four pillars of OOP in C#.
**Answer:**
1. **Encapsulation**: Bundling data and methods together, hiding internal details
   ```csharp
   public class BankAccount
   {
       private decimal balance;  // Hidden from outside
       
       public void Deposit(decimal amount) { balance += amount; }
       public decimal GetBalance() { return balance; }
   }
   ```

2. **Inheritance**: Creating new classes based on existing classes
   ```csharp
   public class Animal
   {
       public virtual void MakeSound() { }
   }
   
   public class Dog : Animal
   {
       public override void MakeSound() { Console.WriteLine("Woof"); }
   }
   ```

3. **Polymorphism**: Same interface, different implementations
   ```csharp
   Animal animal = new Dog();
   animal.MakeSound();  // Calls Dog's MakeSound
   ```

4. **Abstraction**: Hiding complex implementation, showing only essential features
   ```csharp
   public abstract class Shape
   {
       public abstract double CalculateArea();
   }
   ```

### Q8: What is the difference between `abstract class` and `interface`?
**Answer:**

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| **Fields** | Can have fields | Cannot have fields (before C# 8.0) |
| **Access Modifiers** | Can have any access modifier | Public by default |
| **Multiple Inheritance** | Single inheritance | Multiple interface implementation |
| **Implementation** | Can have implementation | No implementation (before C# 8.0) |
| **Constructor** | Can have constructor | Cannot have constructor |
| **Static Members** | Can have static members | Can have static members (C# 8.0+) |

```csharp
// Abstract class
public abstract class Animal
{
    protected string name;  // Can have fields
    
    public Animal(string name) { this.name = name; }  // Constructor
    
    public abstract void MakeSound();  // Abstract method
    public virtual void Sleep() { Console.WriteLine("Sleeping"); }  // Virtual method
}

// Interface
public interface IFlyable
{
    void Fly();  // No implementation
    int MaxAltitude { get; set; }  // Property
}

// C# 8.0+ default interface implementation
public interface IWalkable
{
    void Walk() { Console.WriteLine("Walking"); }  // Default implementation
}
```

### Q9: Explain `virtual`, `override`, and `new` keywords.
**Answer:**
- **`virtual`**: Allows a method to be overridden in derived classes
- **`override`**: Replaces the base class implementation
- **`new`**: Hides the base class member (method hiding)

```csharp
public class BaseClass
{
    public virtual void Method1() { Console.WriteLine("Base Method1"); }
    public void Method2() { Console.WriteLine("Base Method2"); }
}

public class DerivedClass : BaseClass
{
    public override void Method1() { Console.WriteLine("Derived Method1"); }
    public new void Method2() { Console.WriteLine("Derived Method2"); }
}

BaseClass obj = new DerivedClass();
obj.Method1();  // "Derived Method1" - uses override
obj.Method2();  // "Base Method2" - uses base implementation (hiding)
```

### Q10: What is method overloading vs method overriding?
**Answer:**
- **Overloading**: Multiple methods with same name but different parameters (compile-time)
- **Overriding**: Replacing base class method implementation (runtime)

```csharp
// Overloading
public class Calculator
{
    public int Add(int a, int b) { return a + b; }
    public int Add(int a, int b, int c) { return a + b + c; }
    public double Add(double a, double b) { return a + b; }
}

// Overriding
public class Animal
{
    public virtual void MakeSound() { Console.WriteLine("Some sound"); }
}

public class Dog : Animal
{
    public override void MakeSound() { Console.WriteLine("Woof"); }
}
```

### Q11: What are access modifiers in C#?
**Answer:**
- **`public`**: Accessible from anywhere
- **`private`**: Accessible only within the same class
- **`protected`**: Accessible within the class and derived classes
- **`internal`**: Accessible within the same assembly
- **`protected internal`**: Accessible within the same assembly or derived classes
- **`private protected`**: Accessible within the same assembly and derived classes (C# 7.2+)

```csharp
public class Example
{
    public int PublicField;           // Accessible everywhere
    private int PrivateField;         // Only in this class
    protected int ProtectedField;     // This class and derived classes
    internal int InternalField;       // Same assembly
    protected internal int ProtectedInternalField;  // Same assembly or derived
    private protected int PrivateProtectedField;    // Same assembly and derived
}
```

---

## Collections and Generics

### Q12: Explain the main collection types in C#.
**Answer:**

**Non-generic (avoid in modern C#):**
- `ArrayList`, `Hashtable`, `Stack`, `Queue`

**Generic Collections:**
- **`List<T>`**: Dynamic array, indexed access
- **`Dictionary<TKey, TValue>`**: Key-value pairs, fast lookup
- **`HashSet<T>`**: Unique elements, no duplicates
- **`Queue<T>`**: FIFO (First In First Out)
- **`Stack<T>`**: LIFO (Last In First Out)
- **`LinkedList<T>`**: Doubly linked list

```csharp
// List
List<int> numbers = new List<int> { 1, 2, 3 };
numbers.Add(4);

// Dictionary
Dictionary<string, int> ages = new Dictionary<string, int>();
ages["John"] = 30;
ages["Jane"] = 25;

// HashSet
HashSet<int> uniqueNumbers = new HashSet<int> { 1, 2, 2, 3 };  // {1, 2, 3}

// Queue
Queue<string> queue = new Queue<string>();
queue.Enqueue("First");
queue.Enqueue("Second");
string first = queue.Dequeue();  // "First"

// Stack
Stack<string> stack = new Stack<string>();
stack.Push("First");
stack.Push("Second");
string last = stack.Pop();  // "Second"
```

### Q13: What are Generics and why are they useful?
**Answer:**
Generics allow you to define type-safe classes, methods, and interfaces without specifying the actual type until use.

**Benefits:**
- Type safety at compile time
- Performance (no boxing/unboxing)
- Code reusability
- IntelliSense support

```csharp
// Generic class
public class Repository<T>
{
    private List<T> items = new List<T>();
    
    public void Add(T item) { items.Add(item); }
    public T Get(int index) { return items[index]; }
}

// Usage
Repository<string> stringRepo = new Repository<string>();
Repository<int> intRepo = new Repository<int>();

// Generic method
public T Max<T>(T a, T b) where T : IComparable<T>
{
    return a.CompareTo(b) > 0 ? a : b;
}
```

### Q14: What are generic constraints?
**Answer:**
Constraints limit the types that can be used with generics.

```csharp
public class Repository<T> where T : class, new()
{
    // T must be a reference type with parameterless constructor
}

// Common constraints:
// where T : struct          - Value type
// where T : class           - Reference type
// where T : new()           - Has parameterless constructor
// where T : BaseClass       - Inherits from BaseClass
// where T : IInterface      - Implements IInterface
// where T : U               - T derives from U

public class Example<T> where T : IComparable<T>, new()
{
    public T CreateAndCompare()
    {
        T obj1 = new T();
        T obj2 = new T();
        return obj1.CompareTo(obj2) > 0 ? obj1 : obj2;
    }
}
```

---

## LINQ

### Q15: What is LINQ and what are its types?
**Answer:**
LINQ (Language Integrated Query) provides query capabilities directly in C#.

**Types:**
1. **LINQ to Objects**: Query in-memory collections
2. **LINQ to SQL**: Query SQL databases
3. **LINQ to XML**: Query XML documents
4. **LINQ to Entities**: Query Entity Framework

**Syntax:**
- **Query Syntax**: SQL-like syntax
- **Method Syntax**: Extension methods

```csharp
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };

// Query syntax
var evenNumbers = from n in numbers
                 where n % 2 == 0
                 select n;

// Method syntax
var evenNumbers2 = numbers.Where(n => n % 2 == 0);

// Common LINQ methods
var filtered = numbers.Where(n => n > 2);
var projected = numbers.Select(n => n * 2);
var ordered = numbers.OrderByDescending(n => n);
var grouped = numbers.GroupBy(n => n % 2);
var first = numbers.FirstOrDefault(n => n > 10);
var any = numbers.Any(n => n > 10);
var all = numbers.All(n => n > 0);
var sum = numbers.Sum();
var average = numbers.Average();
```

### Q16: Explain deferred execution in LINQ.
**Answer:**
Deferred execution means the query is not executed until the result is enumerated.

```csharp
var numbers = new List<int> { 1, 2, 3, 4, 5 };

// Query is not executed yet
var query = numbers.Where(n => n > 2);

// Query executes here (when enumerated)
numbers.Add(6);
foreach (var num in query)  // Includes 6!
{
    Console.WriteLine(num);
}

// Immediate execution
var list = numbers.Where(n => n > 2).ToList();  // Executes immediately
numbers.Add(7);  // list doesn't include 7
```

**Methods that cause immediate execution:**
- `ToList()`, `ToArray()`, `ToDictionary()`
- `Count()`, `First()`, `Last()`, `Single()`
- `Sum()`, `Average()`, `Max()`, `Min()`

---

## Async/Await and Asynchronous Programming

### Q17: What is async/await and why is it used?
**Answer:**
`async/await` provides a way to write asynchronous code that looks like synchronous code.

**Benefits:**
- Non-blocking I/O operations
- Better UI responsiveness
- Improved scalability

```csharp
// Synchronous (blocks thread)
public string GetData()
{
    return httpClient.GetStringAsync("url").Result;  // Blocks!
}

// Asynchronous (non-blocking)
public async Task<string> GetDataAsync()
{
    return await httpClient.GetStringAsync("url");  // Doesn't block
}

// Multiple async operations
public async Task<List<string>> GetMultipleDataAsync()
{
    var task1 = GetDataAsync("url1");
    var task2 = GetDataAsync("url2");
    var task3 = GetDataAsync("url3");
    
    await Task.WhenAll(task1, task2, task3);
    
    return new List<string> { task1.Result, task2.Result, task3.Result };
}
```

### Q18: What is the difference between `Task` and `Task<T>`?
**Answer:**
- **`Task`**: Represents an asynchronous operation that doesn't return a value
- **`Task<T>`**: Represents an asynchronous operation that returns a value of type T

```csharp
// Task - no return value
public async Task DoSomethingAsync()
{
    await Task.Delay(1000);
    Console.WriteLine("Done");
}

// Task<T> - returns a value
public async Task<string> GetStringAsync()
{
    await Task.Delay(1000);
    return "Result";
}

// Usage
await DoSomethingAsync();
string result = await GetStringAsync();
```

### Q19: What is `ConfigureAwait(false)` and when to use it?
**Answer:**
`ConfigureAwait(false)` tells the runtime not to capture the synchronization context, which can improve performance in library code.

```csharp
// Without ConfigureAwait - captures context (UI thread)
public async Task<string> GetDataAsync()
{
    return await httpClient.GetStringAsync("url");
    // Continues on original context (UI thread)
}

// With ConfigureAwait(false) - doesn't capture context
public async Task<string> GetDataAsync()
{
    return await httpClient.GetStringAsync("url").ConfigureAwait(false);
    // Continues on any thread pool thread
}

// Rule: Use ConfigureAwait(false) in library code, not in UI code
```

### Q20: Explain `async void` and why it should be avoided.
**Answer:**
`async void` should only be used for event handlers. It's dangerous because:
- Exceptions can't be caught
- No way to await completion
- Difficult to test

```csharp
// BAD - async void (except event handlers)
public async void BadMethod()
{
    await Task.Delay(1000);
    throw new Exception();  // Can't catch this!
}

// GOOD - async Task
public async Task GoodMethod()
{
    await Task.Delay(1000);
    throw new Exception();  // Can be caught
}

// OK - Event handlers can be async void
private async void Button_Click(object sender, EventArgs e)
{
    await DoSomethingAsync();
}
```

---

## Exception Handling

### Q21: Explain exception handling in C#.
**Answer:**
Exception handling uses `try-catch-finally` blocks.

```csharp
try
{
    // Code that might throw exception
    int result = 10 / 0;
}
catch (DivideByZeroException ex)
{
    // Handle specific exception
    Console.WriteLine($"Division by zero: {ex.Message}");
}
catch (Exception ex)
{
    // Handle any other exception
    Console.WriteLine($"Error: {ex.Message}");
}
finally
{
    // Always executes (cleanup code)
    Console.WriteLine("Cleanup");
}

// Exception filters (C# 6.0+)
try { }
catch (Exception ex) when (ex.Message.Contains("specific"))
{
    // Only catches if condition is true
}
```

### Q22: What is the difference between `throw` and `throw ex`?
**Answer:**
- **`throw`**: Preserves the original stack trace
- **`throw ex`**: Resets the stack trace (loses original exception location)

```csharp
// BAD - loses stack trace
try
{
    DoSomething();
}
catch (Exception ex)
{
    throw ex;  // Stack trace starts here
}

// GOOD - preserves stack trace
try
{
    DoSomething();
}
catch (Exception ex)
{
    throw;  // Original stack trace preserved
}

// BEST - wraps exception with context
try
{
    DoSomething();
}
catch (Exception ex)
{
    throw new InvalidOperationException("Additional context", ex);
}
```

### Q23: What are custom exceptions?
**Answer:**
Custom exceptions inherit from `Exception` or its derived classes.

```csharp
public class CustomException : Exception
{
    public CustomException() : base() { }
    public CustomException(string message) : base(message) { }
    public CustomException(string message, Exception innerException) 
        : base(message, innerException) { }
}

// Usage
throw new CustomException("Something went wrong");
```

---

## Memory Management and Garbage Collection

### Q24: Explain Garbage Collection in .NET.
**Answer:**
Garbage Collection automatically manages memory by:
1. Identifying unused objects
2. Reclaiming memory
3. Compacting memory

**Generations:**
- **Gen 0**: New objects (short-lived)
- **Gen 1**: Objects that survived Gen 0 collection
- **Gen 2**: Long-lived objects

```csharp
// Force garbage collection (usually not needed)
GC.Collect();
GC.WaitForPendingFinalizers();
GC.Collect();

// Get generation of object
int gen = GC.GetGeneration(myObject);

// Get total memory
long memory = GC.GetTotalMemory(false);
```

### Q25: What is the `using` statement and IDisposable?
**Answer:**
The `using` statement ensures `Dispose()` is called, even if an exception occurs.

```csharp
// Automatic disposal
using (var file = new StreamReader("file.txt"))
{
    string content = file.ReadToEnd();
}  // Dispose() called automatically

// C# 8.0+ using declaration
using var file = new StreamReader("file.txt");
string content = file.ReadToEnd();
// Dispose() called at end of scope

// IDisposable pattern
public class Resource : IDisposable
{
    private bool disposed = false;
    
    public void Dispose()
    {
        Dispose(true);
        GC.SuppressFinalize(this);
    }
    
    protected virtual void Dispose(bool disposing)
    {
        if (!disposed)
        {
            if (disposing)
            {
                // Dispose managed resources
            }
            // Dispose unmanaged resources
            disposed = true;
        }
    }
    
    ~Resource()  // Finalizer
    {
        Dispose(false);
    }
}
```

### Q26: What is boxing and unboxing?
**Answer:**
- **Boxing**: Converting value type to object (heap allocation)
- **Unboxing**: Converting object back to value type

```csharp
// Boxing
int value = 10;
object obj = value;  // Boxing - creates object on heap

// Unboxing
int unboxed = (int)obj;  // Unboxing - extracts value

// Performance impact
// Boxing is expensive - avoid in loops
for (int i = 0; i < 1000000; i++)
{
    object o = i;  // BAD - boxes every iteration
}

// Use generics to avoid boxing
List<int> numbers = new List<int>();  // No boxing
```

---

## Delegates and Events

### Q27: What are delegates?
**Answer:**
Delegates are type-safe function pointers that reference methods.

```csharp
// Delegate declaration
public delegate int MathOperation(int a, int b);

// Delegate instance
MathOperation add = (a, b) => a + b;
MathOperation multiply = (a, b) => a * b;

// Invocation
int result = add(5, 3);  // 8

// Built-in delegates
Action<int> action = (x) => Console.WriteLine(x);
Func<int, int, int> func = (a, b) => a + b;
Predicate<int> predicate = (x) => x > 0;
```

### Q28: What are events and how do they differ from delegates?
**Answer:**
Events are a special type of delegate that provides encapsulation and safety.

```csharp
public class Publisher
{
    // Event declaration
    public event EventHandler SomethingHappened;
    
    // Custom event args
    public event EventHandler<CustomEventArgs> CustomEvent;
    
    protected virtual void OnSomethingHappened()
    {
        SomethingHappened?.Invoke(this, EventArgs.Empty);
    }
}

public class Subscriber
{
    public void Subscribe(Publisher pub)
    {
        pub.SomethingHappened += HandleEvent;
    }
    
    private void HandleEvent(object sender, EventArgs e)
    {
        Console.WriteLine("Event handled");
    }
}

// Usage
var publisher = new Publisher();
var subscriber = new Subscriber();
subscriber.Subscribe(publisher);
```

**Differences:**
- Events can only be invoked from the declaring class
- Events provide better encapsulation
- Events support `+=` and `-=` operators

### Q29: Explain Action, Func, and Predicate delegates.
**Answer:**
These are built-in generic delegates:

```csharp
// Action - no return value (void)
Action action = () => Console.WriteLine("Hello");
Action<int> actionWithParam = (x) => Console.WriteLine(x);
Action<int, string> actionMultiple = (x, s) => Console.WriteLine($"{x}: {s}");

// Func - returns a value (last type parameter is return type)
Func<int> func = () => 42;
Func<int, int> funcSquare = (x) => x * x;
Func<int, int, int> funcAdd = (a, b) => a + b;

// Predicate - returns bool (takes one parameter)
Predicate<int> isPositive = (x) => x > 0;
Predicate<string> isEmpty = (s) => string.IsNullOrEmpty(s);

// Usage
List<int> numbers = new List<int> { -1, 2, -3, 4 };
var positives = numbers.FindAll(isPositive);  // [2, 4]
```

---

## Reflection

### Q30: What is Reflection in C#?
**Answer:**
Reflection allows inspecting and manipulating types, properties, methods at runtime.

```csharp
using System.Reflection;

Type type = typeof(MyClass);

// Get properties
PropertyInfo[] properties = type.GetProperties();
foreach (var prop in properties)
{
    Console.WriteLine($"Property: {prop.Name}, Type: {prop.PropertyType}");
}

// Get methods
MethodInfo[] methods = type.GetMethods();
foreach (var method in methods)
{
    Console.WriteLine($"Method: {method.Name}");
}

// Create instance
object instance = Activator.CreateInstance(type);

// Invoke method
MethodInfo methodInfo = type.GetMethod("MyMethod");
methodInfo.Invoke(instance, new object[] { "parameter" });

// Get attribute
var attribute = type.GetCustomAttribute<MyAttribute>();
```

### Q31: What are the performance implications of Reflection?
**Answer:**
Reflection is slower than direct calls because:
- Runtime type checking
- No compile-time optimization
- Security checks

**Alternatives:**
- Use `Expression Trees` for better performance
- Cache reflection results
- Use `dynamic` keyword (still uses reflection but cleaner syntax)
- Code generation (T4 templates, Source Generators)

```csharp
// Slow - Reflection
MethodInfo method = typeof(MyClass).GetMethod("MyMethod");
method.Invoke(instance, parameters);

// Faster - Expression Trees
Expression<Func<MyClass, int>> expr = x => x.MyMethod();
var compiled = expr.Compile();
int result = compiled(instance);

// Fastest - Direct call
int result = instance.MyMethod();
```

---

## Attributes

### Q32: What are Attributes in C#?
**Answer:**
Attributes provide metadata about code elements (classes, methods, properties).

```csharp
// Built-in attributes
[Serializable]
public class MyClass { }

[Obsolete("Use NewMethod instead")]
public void OldMethod() { }

[Conditional("DEBUG")]
public void DebugMethod() { }

// Custom attribute
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Method)]
public class MyAttribute : Attribute
{
    public string Description { get; set; }
    public int Priority { get; set; }
    
    public MyAttribute(string description)
    {
        Description = description;
    }
}

// Usage
[MyAttribute("Important class", Priority = 1)]
public class ImportantClass { }

// Reading attributes
var attribute = typeof(ImportantClass)
    .GetCustomAttribute<MyAttribute>();
Console.WriteLine(attribute.Description);
```

---

## Threading and Concurrency

### Q33: What is the difference between `Thread`, `Task`, and `async/await`?
**Answer:**

**Thread:**
- Low-level, OS thread
- More control but more complex
- Resource-intensive

**Task:**
- Higher-level abstraction
- Uses thread pool
- Better resource management

**async/await:**
- Syntactic sugar for Task
- Makes asynchronous code readable
- Non-blocking

```csharp
// Thread
Thread thread = new Thread(() => DoWork());
thread.Start();
thread.Join();

// Task
Task task = Task.Run(() => DoWork());
task.Wait();

// async/await
async Task DoWorkAsync()
{
    await Task.Run(() => DoWork());
}
```

### Q34: Explain thread synchronization mechanisms.
**Answer:**

**`lock` statement:**
```csharp
private readonly object lockObject = new object();
private int counter = 0;

public void Increment()
{
    lock (lockObject)
    {
        counter++;
    }
}
```

**`Monitor`:**
```csharp
Monitor.Enter(lockObject);
try
{
    // Critical section
}
finally
{
    Monitor.Exit(lockObject);
}
```

**`Mutex`:**
```csharp
Mutex mutex = new Mutex();
mutex.WaitOne();
try
{
    // Critical section
}
finally
{
    mutex.ReleaseMutex();
}
```

**`Semaphore`:**
```csharp
Semaphore semaphore = new Semaphore(3, 3);  // Allow 3 concurrent
semaphore.WaitOne();
try
{
    // Critical section
}
finally
{
    semaphore.Release();
}
```

**`Interlocked`:**
```csharp
int value = 0;
Interlocked.Increment(ref value);  // Atomic operation
```

### Q35: What is `ThreadPool` and when to use it?
**Answer:**
ThreadPool manages a pool of worker threads, reusing them for multiple tasks.

```csharp
// Queue work to thread pool
ThreadPool.QueueUserWorkItem((state) =>
{
    // Work to do
    DoWork();
});

// Using Task (uses ThreadPool internally)
Task.Run(() => DoWork());

// Benefits:
// - Reuses threads (efficient)
// - Automatic management
// - Optimal for short-lived tasks
```

### Q36: Explain `Concurrent Collections`.
**Answer:**
Thread-safe collections for concurrent access:

```csharp
// ConcurrentDictionary
ConcurrentDictionary<string, int> dict = new ConcurrentDictionary<string, int>();
dict.TryAdd("key", 10);
dict.TryUpdate("key", 20, 10);

// ConcurrentQueue
ConcurrentQueue<int> queue = new ConcurrentQueue<int>();
queue.Enqueue(1);
if (queue.TryDequeue(out int value))
{
    Console.WriteLine(value);
}

// ConcurrentStack
ConcurrentStack<int> stack = new ConcurrentStack<int>();
stack.Push(1);
if (stack.TryPop(out int val))
{
    Console.WriteLine(val);
}

// ConcurrentBag (unordered collection)
ConcurrentBag<int> bag = new ConcurrentBag<int>();
bag.Add(1);
if (bag.TryTake(out int item))
{
    Console.WriteLine(item);
}
```

### Q37: What is `async void` and why should it be avoided?
**Answer:**
(Already covered in Q20, but worth repeating)

`async void` should only be used for event handlers because:
- Exceptions can't be caught
- No way to await completion
- Difficult to test

```csharp
// BAD
public async void BadMethod()
{
    await Task.Delay(1000);
    throw new Exception();  // Can't catch!
}

// GOOD
public async Task GoodMethod()
{
    await Task.Delay(1000);
    throw new Exception();  // Can be caught
}
```

---

## Design Patterns

### Q38: Explain Singleton Pattern in C#.
**Answer:**
Ensures only one instance of a class exists.

```csharp
// Thread-safe Singleton
public class Singleton
{
    private static readonly Lazy<Singleton> instance = 
        new Lazy<Singleton>(() => new Singleton());
    
    private Singleton() { }
    
    public static Singleton Instance => instance.Value;
}

// Double-checked locking (older approach)
public class SingletonOld
{
    private static SingletonOld instance;
    private static readonly object lockObject = new object();
    
    private SingletonOld() { }
    
    public static SingletonOld Instance
    {
        get
        {
            if (instance == null)
            {
                lock (lockObject)
                {
                    if (instance == null)
                    {
                        instance = new SingletonOld();
                    }
                }
            }
            return instance;
        }
    }
}
```

### Q39: Explain Factory Pattern.
**Answer:**
Creates objects without specifying the exact class.

```csharp
// Product interface
public interface IProduct
{
    void DoSomething();
}

// Concrete products
public class ProductA : IProduct
{
    public void DoSomething() => Console.WriteLine("Product A");
}

public class ProductB : IProduct
{
    public void DoSomething() => Console.WriteLine("Product B");
}

// Factory
public class ProductFactory
{
    public IProduct CreateProduct(string type)
    {
        return type switch
        {
            "A" => new ProductA(),
            "B" => new ProductB(),
            _ => throw new ArgumentException("Invalid type")
        };
    }
}

// Usage
var factory = new ProductFactory();
var product = factory.CreateProduct("A");
product.DoSomething();
```

### Q40: Explain Dependency Injection.
**Answer:**
Dependency Injection provides dependencies from outside rather than creating them internally.

```csharp
// Without DI
public class Service
{
    private Repository repository = new Repository();  // Tight coupling
}

// With DI
public class Service
{
    private readonly IRepository repository;
    
    public Service(IRepository repository)  // Dependency injected
    {
        this.repository = repository;
    }
}

// Using DI Container (e.g., Microsoft.Extensions.DependencyInjection)
var services = new ServiceCollection();
services.AddScoped<IRepository, Repository>();
services.AddScoped<Service>();
var provider = services.BuildServiceProvider();
var service = provider.GetService<Service>();
```

---

## Entity Framework

### Q41: What is Entity Framework and its approaches?
**Answer:**
Entity Framework is an ORM (Object-Relational Mapping) framework.

**Approaches:**
1. **Database First**: Generate models from existing database
2. **Code First**: Create models, EF generates database
3. **Model First**: Design in designer, generate both

```csharp
// Code First example
public class User
{
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

public class ApplicationDbContext : DbContext
{
    public DbSet<User> Users { get; set; }
    
    protected override void OnConfiguring(DbContextOptionsBuilder optionsBuilder)
    {
        optionsBuilder.UseSqlServer("connection string");
    }
}

// Usage
using (var context = new ApplicationDbContext())
{
    var user = new User { Name = "John", Email = "john@example.com" };
    context.Users.Add(user);
    context.SaveChanges();
    
    var users = context.Users.Where(u => u.Name == "John").ToList();
}
```

### Q42: Explain LINQ to Entities vs LINQ to Objects.
**Answer:**

**LINQ to Objects:**
- Works with in-memory collections
- Executes immediately
- Full LINQ support

**LINQ to Entities:**
- Translates to SQL
- Deferred execution
- Limited to what can be translated to SQL

```csharp
// LINQ to Objects
var list = new List<int> { 1, 2, 3 };
var result = list.Where(x => x > 1).ToList();  // Executes in memory

// LINQ to Entities
var context = new ApplicationDbContext();
var users = context.Users
    .Where(u => u.Name == "John")  // Translated to SQL
    .ToList();  // Executes SQL query
```

### Q43: What is the difference between `IQueryable` and `IEnumerable`?
**Answer:**

**`IEnumerable<T>`:**
- Works with in-memory data
- Executes in application
- All data loaded into memory

**`IQueryable<T>`:**
- Works with database queries
- Executes on database
- Only requested data loaded

```csharp
// IEnumerable - executes in memory
IEnumerable<User> users = context.Users.ToList();  // Loads all
var filtered = users.Where(u => u.Name == "John");  // Filters in memory

// IQueryable - executes on database
IQueryable<User> query = context.Users;  // No query yet
var filtered = query.Where(u => u.Name == "John");  // Adds WHERE clause
var result = filtered.ToList();  // Executes SQL: SELECT * FROM Users WHERE Name = 'John'
```

---

## ASP.NET Core

### Q44: Explain the ASP.NET Core request pipeline.
**Answer:**
Request pipeline processes HTTP requests through middleware components.

```csharp
public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
{
    // Middleware order matters!
    
    if (env.IsDevelopment())
    {
        app.UseDeveloperExceptionPage();
    }
    
    app.UseHttpsRedirection();
    app.UseStaticFiles();
    app.UseRouting();
    app.UseAuthentication();
    app.UseAuthorization();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}

// Custom middleware
public class CustomMiddleware
{
    private readonly RequestDelegate _next;
    
    public CustomMiddleware(RequestDelegate next)
    {
        _next = next;
    }
    
    public async Task InvokeAsync(HttpContext context)
    {
        // Before request
        await _next(context);
        // After request
    }
}
```

### Q45: Explain Dependency Injection in ASP.NET Core.
**Answer:**
ASP.NET Core has built-in DI container.

```csharp
// Register services
public void ConfigureServices(IServiceCollection services)
{
    services.AddScoped<IUserService, UserService>();
    services.AddSingleton<ICacheService, CacheService>();
    services.AddTransient<IEmailService, EmailService>();
}

// Service lifetimes:
// - Singleton: One instance for entire application
// - Scoped: One instance per HTTP request
// - Transient: New instance every time

// Inject into controller
public class UsersController : ControllerBase
{
    private readonly IUserService _userService;
    
    public UsersController(IUserService userService)
    {
        _userService = userService;
    }
}
```

### Q46: What is the difference between `AddScoped`, `AddSingleton`, and `AddTransient`?
**Answer:**

**`AddTransient`:**
- New instance every time
- Use for lightweight, stateless services

**`AddScoped`:**
- One instance per HTTP request
- Use for services that need request context

**`AddSingleton`:**
- One instance for entire application lifetime
- Use for stateless services or caches

```csharp
services.AddTransient<ITransientService, TransientService>();
services.AddScoped<IScopedService, ScopedService>();
services.AddSingleton<ISingletonService, SingletonService>();
```

### Q47: Explain Model Binding and Validation.
**Answer:**

```csharp
// Model
public class UserModel
{
    [Required]
    [StringLength(100)]
    public string Name { get; set; }
    
    [Required]
    [EmailAddress]
    public string Email { get; set; }
    
    [Range(18, 100)]
    public int Age { get; set; }
}

// Controller
[HttpPost]
public IActionResult CreateUser([FromBody] UserModel model)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }
    
    // Process valid model
    return Ok();
}
```

### Q48: What is Middleware in ASP.NET Core?
**Answer:**
Middleware components handle requests and responses in the pipeline.

```csharp
// Custom middleware
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<LoggingMiddleware> _logger;
    
    public LoggingMiddleware(RequestDelegate next, ILogger<LoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }
    
    public async Task InvokeAsync(HttpContext context)
    {
        _logger.LogInformation($"Request: {context.Request.Path}");
        
        await _next(context);
        
        _logger.LogInformation($"Response: {context.Response.StatusCode}");
    }
}

// Extension method for registration
public static class LoggingMiddlewareExtensions
{
    public static IApplicationBuilder UseLogging(this IApplicationBuilder app)
    {
        return app.UseMiddleware<LoggingMiddleware>();
    }
}

// Usage
app.UseLogging();
```

---

## Advanced Topics

### Q49: What are Extension Methods?
**Answer:**
Extension methods allow adding methods to existing types without modifying them.

```csharp
// Extension method
public static class StringExtensions
{
    public static bool IsValidEmail(this string email)
    {
        return email.Contains("@") && email.Contains(".");
    }
    
    public static string Reverse(this string str)
    {
        return new string(str.Reverse().ToArray());
    }
}

// Usage
string email = "test@example.com";
bool isValid = email.IsValidEmail();  // Extension method
string reversed = email.Reverse();
```

### Q50: Explain `yield return` and `yield break`.
**Answer:**
`yield return` creates an iterator that returns elements one at a time (lazy evaluation).

```csharp
// Iterator method
public IEnumerable<int> GetNumbers()
{
    for (int i = 0; i < 10; i++)
    {
        yield return i;  // Returns one at a time
    }
}

// Usage
foreach (var num in GetNumbers())
{
    Console.WriteLine(num);  // Processes one at a time
}

// yield break - exits iterator
public IEnumerable<int> GetNumbersUntil(int max)
{
    for (int i = 0; i < 100; i++)
    {
        if (i >= max)
            yield break;  // Exit iterator
        
        yield return i;
    }
}

// Benefits:
// - Memory efficient (doesn't load all at once)
// - Lazy evaluation
// - Can handle infinite sequences
```

### Q51: What are Tuples and Value Tuples?
**Answer:**
Tuples allow returning multiple values without creating a class.

```csharp
// Tuple (reference type)
Tuple<int, string> tuple = new Tuple<int, string>(1, "John");
int id = tuple.Item1;
string name = tuple.Item2;

// Value Tuple (value type, C# 7.0+)
(int Id, string Name) valueTuple = (1, "John");
int id2 = valueTuple.Id;
string name2 = valueTuple.Name;

// Named tuple
var person = (Id: 1, Name: "John", Age: 30);
Console.WriteLine(person.Name);

// Return multiple values
public (int Sum, int Product) Calculate(int a, int b)
{
    return (a + b, a * b);
}

var result = Calculate(5, 3);
Console.WriteLine($"Sum: {result.Sum}, Product: {result.Product}");

// Deconstruction
(int sum, int product) = Calculate(5, 3);
var (s, p) = Calculate(5, 3);
```

### Q52: Explain Pattern Matching (C# 7.0+).
**Answer:**
Pattern matching provides more expressive ways to check types and values.

```csharp
// Type pattern
object obj = "Hello";
if (obj is string str)
{
    Console.WriteLine(str.ToUpper());
}

// Switch expressions (C# 8.0+)
var result = obj switch
{
    string s => s.ToUpper(),
    int i => i.ToString(),
    null => "null",
    _ => "unknown"
};

// Property pattern
public bool IsWeekend(DateTime date) => date.DayOfWeek switch
{
    DayOfWeek.Saturday => true,
    DayOfWeek.Sunday => true,
    _ => false
};

// Tuple pattern
var point = (x: 0, y: 0);
var quadrant = point switch
{
    (0, 0) => "Origin",
    (var x, var y) when x > 0 && y > 0 => "Quadrant I",
    (var x, var y) when x < 0 && y > 0 => "Quadrant II",
    _ => "Other"
};
```

### Q53: What are Records (C# 9.0+)?
**Answer:**
Records are immutable reference types with value-based equality.

```csharp
// Record declaration
public record Person(string FirstName, string LastName);

// Usage
var person1 = new Person("John", "Doe");
var person2 = new Person("John", "Doe");

Console.WriteLine(person1 == person2);  // True (value equality)
Console.WriteLine(person1.Equals(person2));  // True

// With expression (creates copy with modifications)
var person3 = person1 with { LastName = "Smith" };

// Record with body
public record Employee(string FirstName, string LastName)
{
    public string FullName => $"{FirstName} {LastName}";
    public int Age { get; init; }
}

// Inheritance
public record Student(string FirstName, string LastName, string School) 
    : Person(FirstName, LastName);
```

### Q54: Explain Nullable Reference Types (C# 8.0+).
**Answer:**
Nullable reference types help prevent null reference exceptions.

```csharp
#nullable enable

// Non-nullable reference (default)
string name = "John";  // Cannot be null
string? nullableName = null;  // Can be null

// Warning if null assigned
string name2 = null;  // Warning!

// Null-forgiving operator
string name3 = null!;  // Suppresses warning

// Null-conditional operator
string? value = GetValue();
int length = value?.Length ?? 0;

// Null-coalescing
string result = value ?? "default";
```

### Q55: What are Init-only Setters (C# 9.0+)?
**Answer:**
Init-only setters allow setting properties only during object initialization.

```csharp
public class Person
{
    public string Name { get; init; }  // Can only be set during initialization
    public int Age { get; init; }
}

// Can set during initialization
var person = new Person { Name = "John", Age = 30 };

// Cannot set after initialization
// person.Name = "Jane";  // Error!

// Useful for immutable objects
public record Product(string Name, decimal Price)
{
    public int Id { get; init; }
}
```

### Q56: Explain Local Functions.
**Answer:**
Local functions are methods defined inside other methods.

```csharp
public int Calculate(int[] numbers)
{
    // Local function
    int Add(int a, int b) => a + b;
    
    int sum = 0;
    foreach (var num in numbers)
    {
        sum = Add(sum, num);
    }
    
    return sum;
}

// Benefits:
// - Encapsulation (only visible in containing method)
// - Can access outer variables
// - Can be async
```

### Q57: What are Expression-bodied Members?
**Answer:**
Shorthand syntax for simple members.

```csharp
public class Example
{
    // Property
    public string Name => "John";
    
    // Method
    public int Add(int a, int b) => a + b;
    
    // Constructor
    private string _name;
    public Example(string name) => _name = name;
    
    // Finalizer
    ~Example() => Console.WriteLine("Finalized");
    
    // Indexer
    private int[] _items = new int[10];
    public int this[int index] => _items[index];
}
```

### Q58: Explain String Interpolation.
**Answer:**
String interpolation provides a cleaner way to format strings.

```csharp
// Old way
string name = "John";
int age = 30;
string message = string.Format("Name: {0}, Age: {1}", name, age);

// String interpolation
string message2 = $"Name: {name}, Age: {age}";

// Expressions
string message3 = $"Next year: {age + 1}";

// Formatting
decimal price = 19.99m;
string formatted = $"Price: {price:C}";  // Currency
string date = $"Date: {DateTime.Now:yyyy-MM-dd}";

// Verbatim string interpolation
string path = $@"C:\Users\{name}\Documents";
```

### Q59: What are Anonymous Types?
**Answer:**
Anonymous types create objects without defining a class.

```csharp
// Anonymous type
var person = new { Name = "John", Age = 30 };
Console.WriteLine(person.Name);

// In LINQ
var query = from u in users
            select new { u.Name, u.Email };

foreach (var item in query)
{
    Console.WriteLine($"{item.Name}: {item.Email}");
}

// Limitations:
// - Read-only properties
// - Reference type
// - Cannot return from methods (use dynamic or object)
```

### Q60: Explain the `nameof` Operator.
**Answer:**
`nameof` returns the name of a variable, type, or member as a string.

```csharp
string name = "John";
Console.WriteLine(nameof(name));  // "name"

public class MyClass
{
    public string Property { get; set; }
    
    public void Method()
    {
        Console.WriteLine(nameof(Property));  // "Property"
        Console.WriteLine(nameof(Method));     // "Method"
    }
}

// Benefits:
// - Refactoring-safe
// - Compile-time checking
// - No magic strings

// Common use cases
throw new ArgumentNullException(nameof(parameter));
OnPropertyChanged(nameof(Property));
```

---

## Additional Important Topics

### Q61: What is the difference between `==` and `Equals()`?
**Answer:**

```csharp
// == operator
// - For value types: compares values
// - For reference types: compares references (unless overloaded)
// - Can be overloaded

// Equals() method
// - Virtual method from Object
// - Can be overridden
// - For value types: compares values (boxed)
// - For reference types: compares references (unless overridden)

int a = 10, b = 10;
Console.WriteLine(a == b);        // True
Console.WriteLine(a.Equals(b));    // True

string s1 = "Hello";
string s2 = "Hello";
Console.WriteLine(s1 == s2);      // True (string overloads ==)
Console.WriteLine(s1.Equals(s2)); // True

object o1 = "Hello";
object o2 = "Hello";
Console.WriteLine(o1 == o2);      // False (reference comparison)
Console.WriteLine(o1.Equals(o2)); // True (string overrides Equals)
```

### Q62: Explain the `using` directive and `using` statement.
**Answer:**

```csharp
// using directive - imports namespace
using System;
using System.Collections.Generic;

// using alias - creates alias for namespace or type
using Dict = System.Collections.Generic.Dictionary<string, int>;

// using static - imports static members
using static System.Math;
double result = Sqrt(16);  // Instead of Math.Sqrt(16)

// using statement - ensures Dispose() is called
using (var file = new StreamReader("file.txt"))
{
    // Use file
}  // Dispose() called automatically

// using declaration (C# 8.0+)
using var file = new StreamReader("file.txt");
// Dispose() called at end of scope
```

### Q63: What is the difference between `String` and `string`?
**Answer:**
`string` is an alias for `System.String`. They are identical.

```csharp
string s1 = "Hello";
String s2 = "Hello";

// Both are the same
Console.WriteLine(s1.GetType() == s2.GetType());  // True

// Convention: Use lowercase aliases for built-in types
string name;      // Preferred
String name2;     // Also works, but less common

// Other aliases:
// int = System.Int32
// bool = System.Boolean
// object = System.Object
// etc.
```

### Q64: Explain the `is` and `as` operators.
**Answer:**

```csharp
// is operator - type checking
object obj = "Hello";
if (obj is string)
{
    Console.WriteLine("It's a string");
}

// Pattern matching with is (C# 7.0+)
if (obj is string str)
{
    Console.WriteLine(str.ToUpper());  // str is already cast
}

// as operator - safe casting (returns null if fails)
object obj2 = "Hello";
string s = obj2 as string;  // Returns string or null
if (s != null)
{
    Console.WriteLine(s);
}

// vs regular cast
string s2 = (string)obj2;  // Throws exception if cast fails
```

### Q65: What are Partial Classes and Methods?
**Answer:**

```csharp
// Partial class - split across multiple files
// File1.cs
public partial class MyClass
{
    public void Method1() { }
}

// File2.cs
public partial class MyClass
{
    public void Method2() { }
}

// Partial method - implementation optional
public partial class MyClass
{
    partial void PartialMethod();  // Declaration
    
    public void CallPartial()
    {
        PartialMethod();  // Only called if implemented
    }
}

// Another file
public partial class MyClass
{
    partial void PartialMethod()  // Implementation
    {
        Console.WriteLine("Implemented");
    }
}

// If not implemented, calls to PartialMethod() are removed by compiler
```

---

## Summary

This document covers comprehensive C# interview questions covering:
- Fundamentals and basics
- Object-oriented programming concepts
- Collections and generics
- LINQ and querying
- Asynchronous programming
- Exception handling
- Memory management
- Delegates and events
- Reflection and attributes
- Threading and concurrency
- Design patterns
- Entity Framework
- ASP.NET Core
- Advanced C# features

Good luck with your interviews! Remember to practice coding examples and understand the underlying concepts, not just memorize answers.

