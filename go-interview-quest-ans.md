# Go (Golang) Interview Questions and Answers

> Based on [roadmap.sh/golang](https://roadmap.sh/golang) and [gobyexample.com](https://gobyexample.com/)

---

## Table of Contents
1. [Introduction to Go](#introduction-to-go)
2. [Basic Syntax and Fundamentals](#basic-syntax-and-fundamentals)
3. [Data Types and Variables](#data-types-and-variables)
4. [Control Flow](#control-flow)
5. [Functions](#functions)
6. [Data Structures](#data-structures)
7. [Pointers](#pointers)
8. [Structs and Methods](#structs-and-methods)
9. [Interfaces](#interfaces)
10. [Error Handling](#error-handling)
11. [Concurrency](#concurrency)
12. [Channels](#channels)
13. [Goroutines](#goroutines)
14. [Packages and Modules](#packages-and-modules)
15. [String Operations](#string-operations)
16. [File Operations](#file-operations)
17. [JSON and XML](#json-and-xml)
18. [HTTP Client and Server](#http-client-and-server)
19. [Testing](#testing)
20. [Advanced Topics](#advanced-topics)

---

## Introduction to Go

### Q1. What is Go (Golang)? (Easy)

**Answer:**
Go, also known as Golang, is an open-source programming language developed at Google by developers like Rob Pike, Ken Thompson, and Robert Griesemer. It was designed with simplicity, efficiency, and performance in mind.

**Key Features:**
- Compiled language (translated to machine code before execution)
- Strong standard library
- Built-in garbage collection
- Excellent concurrency support (goroutines and channels)
- Fast compilation and execution
- Clean and simple syntax
- Static typing with type inference
- Cross-platform support

**Use Cases:**
- Backend development
- Microservices
- API development
- Cloud-native applications
- DevOps tools
- Network programming
- System programming

---

### Q2. What is the difference between Go and Golang? (Easy)

**Answer:**
Go and Golang refer to the same programming language. "Go" is the official name, while "Golang" is a popular nickname that emerged because:
1. The official domain is `golang.org`
2. Searching for "go" online returns many irrelevant results
3. It helps distinguish the language from other uses of the word "go"

Both terms are used interchangeably in the industry.

---

### Q3. What are the main design principles of Go? (Medium)

**Answer:**
Go was designed with several key principles:

1. **Simplicity:** Minimal syntax, easy to read and write
2. **Efficiency:** Fast compilation and execution
3. **Concurrency:** Built-in support for concurrent programming
4. **Garbage Collection:** Automatic memory management
5. **Static Typing:** Type safety with type inference
6. **Fast Compilation:** Quick build times
7. **Standard Library:** Comprehensive built-in packages
8. **Opinionated:** Few ways to do things (reduces confusion)

**Philosophy:**
- "Less is exponentially more" - simplicity over features
- Explicit over implicit
- Composition over inheritance
- Concurrency as a first-class citizen

---

### Q4. Is Go difficult to learn? (Easy)

**Answer:**
Go is considered relatively easy to learn, especially for developers with programming experience. Reasons:

**Advantages:**
- Simple, clean syntax (minimal keywords)
- Small language specification
- Excellent documentation
- Strong community support
- No complex features like inheritance or generics (in older versions)

**Challenges:**
- Understanding goroutines and channels (concurrency model)
- Working with pointers
- Error handling patterns
- Interface design

**For Beginners:**
- Easier than C++ or Rust
- More structured than Python/JavaScript
- Good balance between simplicity and power

---

### Q5. What makes Go suitable for backend development? (Medium)

**Answer:**
Go excels in backend development due to:

1. **Performance:** Compiled language with fast execution
2. **Concurrency:** Excellent for handling multiple requests
3. **Standard Library:** Rich HTTP and networking support
4. **Cross-platform:** Single binary deployment
5. **Low Memory Footprint:** Efficient resource usage
6. **Fast Compilation:** Quick development cycles
7. **Strong Tooling:** Built-in testing, formatting, and profiling

**Companies Using Go:**
- Google, Uber, Dropbox, Docker, Kubernetes, Netflix, Twitch

---

## Basic Syntax and Fundamentals

### Q6. Write a "Hello World" program in Go. (Easy)

**Answer:**
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

**Explanation:**
- `package main`: Declares this as an executable program
- `import "fmt"`: Imports the format package for I/O
- `func main()`: Entry point of the program
- `fmt.Println()`: Prints to standard output

---

### Q7. What are the basic value types in Go? (Easy)

**Answer:**
Go has several basic value types:

```go
// Boolean
var b bool = true

// String
var s string = "Hello"

// Integers (signed and unsigned)
var i int = 42          // Platform-dependent size
var i8 int8 = 127       // 8-bit signed
var i16 int16 = 32767   // 16-bit signed
var i32 int32 = 2147483647  // 32-bit signed
var i64 int64 = 9223372036854775807  // 64-bit signed

var u uint = 42         // Unsigned
var u8 uint8 = 255      // 8-bit unsigned (byte)
var u16 uint16 = 65535  // 16-bit unsigned
var u32 uint32          // 32-bit unsigned
var u64 uint64          // 64-bit unsigned

// Floating point
var f32 float32 = 3.14
var f64 float64 = 3.141592653589793

// Complex numbers
var c64 complex64 = 1 + 2i
var c128 complex128 = 1 + 2i

// Byte and Rune
var by byte = 'A'       // Alias for uint8
var r rune = '世'        // Alias for int32 (Unicode code point)
```

---

### Q8. How do you declare variables in Go? (Easy)

**Answer:**
Go provides multiple ways to declare variables:

```go
// 1. Explicit type declaration
var name string = "John"

// 2. Type inference
var name = "John"

// 3. Short variable declaration (inside functions)
name := "John"

// 4. Multiple variables
var x, y int = 1, 2
var a, b = "hello", true
x, y := 1, 2

// 5. Variable block
var (
    name string = "John"
    age  int    = 30
    city        = "NYC"  // Type inferred
)

// 6. Zero values (default values)
var i int        // 0
var f float64    // 0.0
var b bool       // false
var s string     // ""
```

**Zero Values:**
- Numbers: `0`
- Booleans: `false`
- Strings: `""`
- Pointers, slices, maps, channels, functions: `nil`

---

### Q9. What are constants in Go? (Easy)

**Answer:**
Constants are immutable values declared with the `const` keyword:

```go
// Basic constant
const Pi = 3.14159

// Typed constant
const StatusOK int = 200

// Multiple constants
const (
    StatusOK       = 200
    StatusNotFound = 404
    StatusError    = 500
)

// Iota (creates enumerated constants)
const (
    Sunday = iota  // 0
    Monday         // 1
    Tuesday        // 2
    Wednesday      // 3
    Thursday       // 4
    Friday         // 5
    Saturday       // 6
)

// Iota with expressions
const (
    KB = 1024
    MB = KB * 1024
    GB = MB * 1024
)
```

**Key Points:**
- Must be known at compile time
- Cannot be reassigned
- Can be untyped (can be used with different types)

---

### Q10. Explain the difference between `var` and `:=` in Go. (Medium)

**Answer:**

```go
// var: Can be used at package level or function level
var globalVar string = "global"  // Package level

func example() {
    var localVar string = "local"  // Function level
    // Can be reassigned
    localVar = "changed"
}

// := Short variable declaration
// - Only inside functions
// - Declares and assigns in one step
// - Type is inferred
func example2() {
    name := "John"  // Declares and assigns
    // name := "Jane"  // Error: no new variables on left side
    name = "Jane"   // OK: assignment
    age, city := 30, "NYC"  // Multiple variables
}
```

**Differences:**
| Feature | `var` | `:=` |
|---------|-------|------|
| Scope | Package or function | Function only |
| Reassignment | Yes | Yes (but can't redeclare) |
| Type inference | Optional | Required |
| Zero value | Can declare without value | Must assign value |

---

## Control Flow

### Q11. How does the `for` loop work in Go? (Easy)

**Answer:**
Go has only one looping construct: `for`. It can be used in multiple ways:

```go
// 1. Traditional for loop
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// 2. While-style loop
i := 0
for i < 10 {
    fmt.Println(i)
    i++
}

// 3. Infinite loop
for {
    // Break with condition
    if condition {
        break
    }
}

// 4. Range over slice
numbers := []int{1, 2, 3, 4, 5}
for index, value := range numbers {
    fmt.Printf("Index: %d, Value: %d\n", index, value)
}

// 5. Range over map
m := map[string]int{"a": 1, "b": 2}
for key, value := range m {
    fmt.Printf("Key: %s, Value: %d\n", key, value)
}

// 6. Range over string (iterates over runes)
for i, r := range "Hello, 世界" {
    fmt.Printf("Index: %d, Rune: %c\n", i, r)
}

// 7. Skip index or value
for _, value := range numbers {  // Skip index
    fmt.Println(value)
}

for index := range numbers {  // Skip value
    fmt.Println(index)
}
```

---

### Q12. Explain `if/else` statements in Go. (Easy)

**Answer:**
Go's `if` statement can include an initialization statement:

```go
// Basic if
if x > 0 {
    fmt.Println("Positive")
}

// If-else
if x > 0 {
    fmt.Println("Positive")
} else {
    fmt.Println("Non-positive")
}

// If-else if-else
if x > 0 {
    fmt.Println("Positive")
} else if x < 0 {
    fmt.Println("Negative")
} else {
    fmt.Println("Zero")
}

// If with initialization (common pattern)
if err := doSomething(); err != nil {
    fmt.Println("Error:", err)
}

// Variables declared in if are scoped to if-else blocks
if num := 9; num < 0 {
    fmt.Println("Negative")
} else if num < 10 {
    fmt.Println("Single digit")
} else {
    fmt.Println("Multiple digits")
}
// num is not accessible here
```

**Key Points:**
- No parentheses around condition (required in other languages)
- Braces are mandatory
- Can declare variables in the condition

---

### Q13. How does `switch` work in Go? (Medium)

**Answer:**
Go's `switch` is more flexible than in other languages:

```go
// 1. Basic switch
switch day {
case "Monday":
    fmt.Println("Start of week")
case "Friday":
    fmt.Println("End of week")
default:
    fmt.Println("Midweek")
}

// 2. Switch with multiple values
switch day {
case "Saturday", "Sunday":
    fmt.Println("Weekend")
case "Monday", "Tuesday", "Wednesday", "Thursday", "Friday":
    fmt.Println("Weekday")
}

// 3. Switch with initialization
switch os := runtime.GOOS; os {
case "darwin":
    fmt.Println("macOS")
case "linux":
    fmt.Println("Linux")
default:
    fmt.Println("Other")
}

// 4. Switch without condition (like if-else chain)
t := time.Now()
switch {
case t.Hour() < 12:
    fmt.Println("Morning")
case t.Hour() < 17:
    fmt.Println("Afternoon")
default:
    fmt.Println("Evening")
}

// 5. Type switch
var i interface{} = "hello"
switch v := i.(type) {
case int:
    fmt.Printf("Integer: %d\n", v)
case string:
    fmt.Printf("String: %s\n", v)
default:
    fmt.Printf("Unknown type\n")
}

// 6. Fallthrough (explicit, not automatic)
switch x {
case 1:
    fmt.Println("One")
    fallthrough  // Continues to next case
case 2:
    fmt.Println("Two")
}
```

**Key Differences from Other Languages:**
- No automatic fallthrough (must use `fallthrough` explicitly)
- Can switch on any type, not just integers
- Can use expressions in cases
- Can omit condition for if-else style

---

## Functions

### Q14. How do you define and call functions in Go? (Easy)

**Answer:**

```go
// Basic function
func greet(name string) {
    fmt.Printf("Hello, %s!\n", name)
}

// Function with return value
func add(a int, b int) int {
    return a + b
}

// Multiple return values (Go idiom)
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("division by zero")
    }
    return a / b, nil
}

// Named return values
func calculate(x, y int) (sum int, product int) {
    sum = x + y      // Assignment, not declaration
    product = x * y
    return           // Naked return (returns named values)
}

// Variadic function
func sum(numbers ...int) int {
    total := 0
    for _, num := range numbers {
        total += num
    }
    return total
}

// Function as value
var multiply = func(x, y int) int {
    return x * y
}

// Higher-order function
func apply(fn func(int, int) int, a, b int) int {
    return fn(a, b)
}

// Usage
func main() {
    greet("Alice")
    result := add(5, 3)
    quotient, err := divide(10, 2)
    sum, prod := calculate(3, 4)
    total := sum(1, 2, 3, 4, 5)
    result2 := apply(multiply, 5, 6)
}
```

---

### Q15. What are variadic functions? (Medium)

**Answer:**
Variadic functions accept a variable number of arguments:

```go
// Variadic parameter (must be last)
func sum(numbers ...int) int {
    total := 0
    for _, num := range numbers {
        total += num
    }
    return total
}

// Usage
result := sum(1, 2, 3)           // 6
result = sum(1, 2, 3, 4, 5)      // 15
result = sum()                   // 0

// Passing slice to variadic function
numbers := []int{1, 2, 3, 4}
result = sum(numbers...)  // Spread operator

// Multiple parameters with variadic
func printInfo(prefix string, values ...interface{}) {
    fmt.Print(prefix + ": ")
    for _, v := range values {
        fmt.Print(v, " ")
    }
    fmt.Println()
}

printInfo("Numbers", 1, 2, 3)
printInfo("Mixed", "hello", 42, true)
```

**Key Points:**
- Variadic parameter must be the last parameter
- Inside function, it's a slice
- Can pass slice using `...` spread operator
- Can be empty (zero-length slice)

---

### Q16. What are closures in Go? (Medium)

**Answer:**
Closures are functions that capture variables from their surrounding scope:

```go
// Basic closure
func makeCounter() func() int {
    count := 0
    return func() int {
        count++
        return count
    }
}

func main() {
    counter1 := makeCounter()
    counter2 := makeCounter()
    
    fmt.Println(counter1())  // 1
    fmt.Println(counter1())  // 2
    fmt.Println(counter2())  // 1 (independent)
    fmt.Println(counter1())  // 3
}

// Closure with parameters
func makeMultiplier(factor int) func(int) int {
    return func(x int) int {
        return x * factor
    }
}

func main() {
    double := makeMultiplier(2)
    triple := makeMultiplier(3)
    
    fmt.Println(double(5))   // 10
    fmt.Println(triple(5))   // 15
}

// Common pattern: Function that returns a function
func logger(prefix string) func(string) {
    return func(msg string) {
        fmt.Printf("[%s] %s\n", prefix, msg)
    }
}

func main() {
    infoLog := logger("INFO")
    errorLog := logger("ERROR")
    
    infoLog("Application started")
    errorLog("Something went wrong")
}
```

**Key Points:**
- Closures capture variables by reference
- Each closure maintains its own captured variables
- Useful for function factories and callbacks

---

### Q17. Explain recursion in Go. (Easy)

**Answer:**
Go supports recursive function calls:

```go
// Factorial
func factorial(n int) int {
    if n <= 1 {
        return 1
    }
    return n * factorial(n-1)
}

// Fibonacci
func fibonacci(n int) int {
    if n <= 1 {
        return n
    }
    return fibonacci(n-1) + fibonacci(n-2)
}

// Binary search (recursive)
func binarySearch(arr []int, target, left, right int) int {
    if left > right {
        return -1
    }
    
    mid := (left + right) / 2
    if arr[mid] == target {
        return mid
    } else if arr[mid] > target {
        return binarySearch(arr, target, left, mid-1)
    } else {
        return binarySearch(arr, target, mid+1, right)
    }
}

// Tree traversal
type Node struct {
    Value int
    Left  *Node
    Right *Node
}

func inorderTraversal(root *Node) []int {
    if root == nil {
        return []int{}
    }
    result := inorderTraversal(root.Left)
    result = append(result, root.Value)
    result = append(result, inorderTraversal(root.Right)...)
    return result
}
```

---

## Data Structures

### Q18. What are arrays in Go? (Easy)

**Answer:**
Arrays are fixed-size sequences of elements of the same type:

```go
// Array declaration
var arr [5]int                    // Zero-initialized
arr := [5]int{1, 2, 3, 4, 5}      // Initialized
arr := [...]int{1, 2, 3, 4, 5}    // Size inferred

// Array operations
arr[0] = 10                       // Access/modify
length := len(arr)                // Length
fmt.Println(arr[0])               // Access element

// Multi-dimensional array
var matrix [3][3]int
matrix[0][0] = 1

// Array is a value type (copied, not referenced)
arr1 := [3]int{1, 2, 3}
arr2 := arr1  // Copy
arr2[0] = 99
fmt.Println(arr1[0])  // Still 1

// Array comparison
arr3 := [3]int{1, 2, 3}
arr4 := [3]int{1, 2, 3}
fmt.Println(arr3 == arr4)  // true (if elements are equal)
```

**Key Points:**
- Fixed size (part of type)
- Value type (copied when assigned)
- Size must be compile-time constant
- Rarely used directly (slices are preferred)

---

### Q19. What are slices in Go? (Medium)

**Answer:**
Slices are dynamic, flexible views into arrays:

```go
// Slice declaration
var s []int                       // nil slice
s := []int{1, 2, 3}               // Literal
s := make([]int, 5)               // Length 5, capacity 5
s := make([]int, 5, 10)           // Length 5, capacity 10

// From array
arr := [5]int{1, 2, 3, 4, 5}
s := arr[1:4]                     // [2, 3, 4]

// Slice operations
s = append(s, 6)                  // Append
length := len(s)                  // Length
capacity := cap(s)                // Capacity
s[0] = 10                         // Modify element

// Slice is a reference type
s1 := []int{1, 2, 3}
s2 := s1                          // Same underlying array
s2[0] = 99
fmt.Println(s1[0])                // 99 (changed!)

// Copying slices
s3 := make([]int, len(s1))
copy(s3, s1)                      // Deep copy

// Slicing operations
s := []int{0, 1, 2, 3, 4, 5}
s[1:4]    // [1, 2, 3]
s[:3]     // [0, 1, 2]
s[3:]     // [3, 4, 5]
s[:]      // [0, 1, 2, 3, 4, 5] (full slice)

// Iterating
for i, v := range s {
    fmt.Printf("Index: %d, Value: %d\n", i, v)
}
```

**Slice Internals:**
- Pointer to underlying array
- Length (current elements)
- Capacity (maximum elements without reallocation)

---

### Q20. Explain the difference between arrays and slices. (Medium)

**Answer:**

| Feature | Array | Slice |
|---------|-------|-------|
| Size | Fixed (compile-time) | Dynamic (runtime) |
| Type | `[n]T` | `[]T` |
| Value/Reference | Value type (copied) | Reference type (points to array) |
| Declaration | `var arr [5]int` | `var s []int` or `s := []int{}` |
| Length | Part of type | Can grow/shrink |
| Comparison | Can compare with `==` | Cannot compare with `==` |
| Usage | Rare | Common |
| Memory | Stack (small) or heap | Always heap |

```go
// Array example
arr := [3]int{1, 2, 3}
arr2 := arr        // Copy
arr2[0] = 99
fmt.Println(arr[0])  // 1 (unchanged)

// Slice example
s := []int{1, 2, 3}
s2 := s            // Reference
s2[0] = 99
fmt.Println(s[0])    // 99 (changed!)
```

---

### Q21. What are maps in Go? (Medium)

**Answer:**
Maps are key-value data structures (hash tables):

```go
// Map declaration
var m map[string]int              // nil map
m := make(map[string]int)         // Empty map
m := map[string]int{              // Literal
    "apple":  5,
    "banana": 3,
}

// Operations
m["orange"] = 4                   // Add/update
value := m["apple"]               // Get (returns zero value if not found)
value, exists := m["banana"]      // Check existence
delete(m, "apple")                // Delete

// Iteration
for key, value := range m {
    fmt.Printf("%s: %d\n", key, value)
}

// Map of slices
m2 := map[string][]int{
    "even": {2, 4, 6},
    "odd":  {1, 3, 5},
}

// Map as set (using bool values)
set := make(map[int]bool)
set[1] = true
set[2] = true
if set[1] {
    fmt.Println("1 is in set")
}
```

**Key Points:**
- Keys must be comparable types
- Zero value is `nil`
- Not safe for concurrent access (use `sync.Map` or mutex)
- Order is not guaranteed
- Reference type

---

### Q22. How do you work with nil slices and maps? (Medium)

**Answer:**

```go
// Nil slice
var s []int
fmt.Println(s == nil)        // true
fmt.Println(len(s))          // 0
s = append(s, 1)            // OK: append works with nil slice

// Empty slice (not nil)
s2 := []int{}
fmt.Println(s2 == nil)       // false
fmt.Println(len(s2))         // 0

// Nil map
var m map[string]int
fmt.Println(m == nil)        // true
// m["key"] = 1              // PANIC: assignment to nil map
m = make(map[string]int)     // Initialize
m["key"] = 1                 // OK now

// Checking nil
if s == nil {
    fmt.Println("Slice is nil")
}

if m == nil {
    fmt.Println("Map is nil")
}

// Safe map operations
if value, ok := m["key"]; ok {
    fmt.Println("Value:", value)
} else {
    fmt.Println("Key not found")
}
```

**Best Practices:**
- Always initialize maps before use
- Nil slices are safe for `append`
- Check for nil before operations
- Use `make()` to initialize maps

---

## Pointers

### Q23. What are pointers in Go? (Medium)

**Answer:**
Pointers store the memory address of a value:

```go
// Pointer declaration
var p *int                    // Pointer to int
x := 42
p = &x                        // Address of x

// Dereferencing
fmt.Println(*p)               // 42 (value at address)
*p = 21                       // Modify through pointer
fmt.Println(x)                // 21 (x changed)

// Pointer to pointer
pp := &p
fmt.Println(**pp)             // 21

// Function with pointer parameter
func increment(p *int) {
    *p++
}

x := 5
increment(&x)
fmt.Println(x)                // 6

// Returning pointer
func newInt() *int {
    x := 42
    return &x                 // Returns address (x escapes to heap)
}

// Pointer to struct
type Person struct {
    Name string
    Age  int
}

p := &Person{Name: "Alice", Age: 30}
p.Age = 31                    // Shorthand: (*p).Age = 31
```

**Key Points:**
- `&` gets address
- `*` dereferences pointer
- Zero value is `nil`
- No pointer arithmetic (unlike C)

---

### Q24. When should you use pointers in Go? (Medium)

**Answer:**
Use pointers when:

1. **Modifying function parameters:**
```go
func swap(a, b *int) {
    *a, *b = *b, *a
}
```

2. **Avoiding large value copies:**
```go
type LargeStruct struct {
    // Many fields
}

func process(s *LargeStruct) {  // Pass pointer, not copy
    // ...
}
```

3. **Optional/nullable values:**
```go
func findUser(id int) (*User, error) {
    // Returns nil if not found
}
```

4. **Sharing data:**
```go
type Counter struct {
    count int
}

func (c *Counter) Increment() {  // Method receiver
    c.count++
}
```

**Avoid pointers when:**
- Working with small values (int, bool, etc.)
- Need value semantics
- Want immutability

---

## Structs and Methods

### Q25. What are structs in Go? (Easy)

**Answer:**
Structs are composite types that group related data:

```go
// Struct definition
type Person struct {
    Name string
    Age  int
    City string
}

// Creating structs
p1 := Person{"Alice", 30, "NYC"}              // Positional
p2 := Person{Name: "Bob", Age: 25, City: "LA"} // Named fields
p3 := Person{Name: "Charlie"}                  // Partial (others zero-valued)

// Accessing fields
fmt.Println(p1.Name)
p1.Age = 31

// Pointer to struct
p4 := &Person{Name: "David", Age: 28}
p4.City = "SF"  // Shorthand: (*p4).City = "SF"

// Anonymous struct
anon := struct {
    X int
    Y int
}{X: 1, Y: 2}

// Embedded structs
type Address struct {
    Street string
    City   string
}

type Employee struct {
    Person          // Embedded
    Address         // Embedded
    Salary float64
}

e := Employee{
    Person:  Person{Name: "Alice"},
    Address: Address{City: "NYC"},
    Salary:  50000,
}
fmt.Println(e.Name)   // Access embedded field
fmt.Println(e.City)   // Access embedded field
```

---

### Q26. What are methods in Go? (Medium)

**Answer:**
Methods are functions with a receiver:

```go
type Rectangle struct {
    Width  float64
    Height float64
}

// Value receiver
func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

// Pointer receiver
func (r *Rectangle) Scale(factor float64) {
    r.Width *= factor
    r.Height *= factor
}

// Usage
rect := Rectangle{Width: 10, Height: 5}
area := rect.Area()           // 50
rect.Scale(2)                 // Modifies rect
fmt.Println(rect.Area())       // 200

// Method on non-struct type
type MyInt int

func (m MyInt) Double() MyInt {
    return m * 2
}

value := MyInt(5)
fmt.Println(value.Double())   // 10
```

**Value vs Pointer Receiver:**
- Value receiver: Operates on copy (doesn't modify original)
- Pointer receiver: Operates on original (can modify)

**When to use:**
- Pointer receiver: When method needs to modify receiver or receiver is large
- Value receiver: When method doesn't modify receiver

---

### Q27. What is struct embedding? (Medium)

**Answer:**
Struct embedding allows one struct to include another without explicit field names:

```go
type Animal struct {
    Name string
    Age  int
}

func (a Animal) Speak() {
    fmt.Println("Some sound")
}

// Dog embeds Animal
type Dog struct {
    Animal        // Embedded (not Animal Animal)
    Breed string
}

// Cat embeds Animal
type Cat struct {
    Animal
    Color string
}

// Usage
dog := Dog{
    Animal: Animal{Name: "Buddy", Age: 3},
    Breed:  "Golden Retriever",
}

fmt.Println(dog.Name)         // Access embedded field
dog.Speak()                   // Access embedded method

// Method overriding
func (d Dog) Speak() {
    fmt.Println("Woof!")
}

dog.Speak()                   // "Woof!" (overridden)
```

**Key Points:**
- Promotes embedded fields/methods to outer struct
- Enables composition over inheritance
- Can override embedded methods
- Similar to mixins in other languages

---

## Interfaces

### Q28. What are interfaces in Go? (Medium)

**Answer:**
Interfaces define behavior (methods) that types must implement:

```go
// Interface definition
type Shape interface {
    Area() float64
    Perimeter() float64
}

// Types implementing interface
type Rectangle struct {
    Width, Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

func (r Rectangle) Perimeter() float64 {
    return 2 * (r.Width + r.Height)
}

type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return math.Pi * c.Radius * c.Radius
}

func (c Circle) Perimeter() float64 {
    return 2 * math.Pi * c.Radius
}

// Function accepting interface
func printArea(s Shape) {
    fmt.Printf("Area: %.2f\n", s.Area())
}

// Usage
rect := Rectangle{Width: 10, Height: 5}
circle := Circle{Radius: 5}

printArea(rect)    // Works
printArea(circle)  // Works

// Empty interface (accepts any type)
func printValue(v interface{}) {
    fmt.Println(v)
}

// Type assertion
var i interface{} = "hello"
s := i.(string)           // Assertion
s, ok := i.(string)       // Safe assertion
```

**Key Points:**
- Implicit implementation (no explicit declaration)
- Interface satisfied if type has all methods
- Empty interface `interface{}` accepts any type
- Used for polymorphism

---

### Q29. Explain the empty interface in Go. (Medium)

**Answer:**
The empty interface `interface{}` accepts any type:

```go
// Empty interface
var i interface{}

i = 42
i = "hello"
i = true
i = []int{1, 2, 3}

// Function accepting any type
func printAnything(v interface{}) {
    fmt.Println(v)
}

// Type switch
func processValue(v interface{}) {
    switch val := v.(type) {
    case int:
        fmt.Printf("Integer: %d\n", val)
    case string:
        fmt.Printf("String: %s\n", val)
    case bool:
        fmt.Printf("Boolean: %t\n", val)
    default:
        fmt.Printf("Unknown type: %T\n", val)
    }
}

// Type assertion
var x interface{} = "hello"
s := x.(string)        // Assert to string
n, ok := x.(int)       // Safe assertion (ok is false)

// Common pattern: JSON unmarshaling
var result interface{}
json.Unmarshal(data, &result)
```

**Modern Alternative (Go 1.18+):**
```go
// Use 'any' alias (Go 1.18+)
func printAnything(v any) {  // Same as interface{}
    fmt.Println(v)
}
```

---

### Q30. What is the difference between value and pointer receivers in methods? (Tough)

**Answer:**

```go
type Counter struct {
    value int
}

// Value receiver
func (c Counter) Increment() {
    c.value++  // Modifies copy, not original
}

// Pointer receiver
func (c *Counter) Decrement() {
    c.value--  // Modifies original
}

func main() {
    c := Counter{value: 0}
    c.Increment()
    fmt.Println(c.value)  // 0 (unchanged!)
    
    c.Decrement()
    fmt.Println(c.value)  // -1 (changed)
}
```

**Rules:**
1. **Value receiver:** Method operates on copy
2. **Pointer receiver:** Method operates on original
3. **Interface satisfaction:** Both can satisfy interface
4. **Consistency:** Use same receiver type for all methods

**When to use pointer receiver:**
- Method modifies receiver
- Receiver is large (avoid copying)
- Consistency with other methods

**When to use value receiver:**
- Method doesn't modify receiver
- Receiver is small
- Want value semantics

---

## Error Handling

### Q31. How does error handling work in Go? (Medium)

**Answer:**
Go uses explicit error returns (no exceptions):

```go
// Error is an interface
type error interface {
    Error() string
}

// Creating errors
import "errors"

err := errors.New("something went wrong")
err := fmt.Errorf("error: %v", value)

// Function returning error
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("division by zero")
    }
    return a / b, nil
}

// Error handling
result, err := divide(10, 2)
if err != nil {
    fmt.Println("Error:", err)
    return
}
fmt.Println("Result:", result)

// Common pattern
if err != nil {
    return err  // Propagate error
}

// Multiple errors
func process() error {
    if err := step1(); err != nil {
        return fmt.Errorf("step1 failed: %w", err)
    }
    if err := step2(); err != nil {
        return fmt.Errorf("step2 failed: %w", err)
    }
    return nil
}
```

**Key Points:**
- Errors are values
- Explicit error checking
- No try-catch
- `nil` means no error

---

### Q32. How do you create custom errors? (Medium)

**Answer:**

```go
// 1. Custom error type
type ValidationError struct {
    Field   string
    Message string
}

func (e *ValidationError) Error() string {
    return fmt.Sprintf("validation error on %s: %s", e.Field, e.Message)
}

// 2. Error with additional methods
type NotFoundError struct {
    Resource string
    ID       string
}

func (e *NotFoundError) Error() string {
    return fmt.Sprintf("%s with ID %s not found", e.Resource, e.ID)
}

func (e *NotFoundError) IsNotFound() bool {
    return true
}

// 3. Using errors.Is and errors.As (Go 1.13+)
var ErrNotFound = errors.New("not found")

func findUser(id string) (*User, error) {
    // ...
    return nil, ErrNotFound
}

// Checking
user, err := findUser("123")
if errors.Is(err, ErrNotFound) {
    fmt.Println("User not found")
}

// Type assertion
var validationErr *ValidationError
if errors.As(err, &validationErr) {
    fmt.Println("Field:", validationErr.Field)
}

// Wrapping errors
func process() error {
    if err := doSomething(); err != nil {
        return fmt.Errorf("process failed: %w", err)  // Wrap
    }
    return nil
}
```

---

### Q33. Explain panic and recover in Go. (Tough)

**Answer:**
Panic stops normal execution, recover can catch panics:

```go
// Panic
func riskyFunction() {
    panic("something went wrong")
}

// Recover (only in deferred function)
func safeFunction() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered from panic:", r)
        }
    }()
    
    riskyFunction()
    fmt.Println("This won't execute")
}

// Real-world example
func divide(a, b int) (result int) {
    defer func() {
        if r := recover(); r != nil {
            result = 0  // Set default value
            fmt.Println("Recovered:", r)
        }
    }()
    
    if b == 0 {
        panic("division by zero")
    }
    return a / b
}

// Best practices
// 1. Don't use panic for normal errors
// 2. Use recover only in specific cases (defer, goroutines)
// 3. Panic for programming errors, not user errors
```

**When to use:**
- **Panic:** Programming errors, unrecoverable situations
- **Recover:** In deferred functions, goroutine boundaries
- **Avoid:** Normal error handling (use error returns)

---

### Q34. What is defer in Go? (Medium)

**Answer:**
`defer` schedules a function call to execute after the surrounding function returns:

```go
// Basic defer
func example() {
    defer fmt.Println("World")
    fmt.Println("Hello")
}
// Output: Hello\nWorld

// Multiple defers (LIFO - Last In First Out)
func example2() {
    defer fmt.Println("First")
    defer fmt.Println("Second")
    defer fmt.Println("Third")
}
// Output: Third\nSecond\nFirst

// Common use case: Closing files
func readFile(filename string) error {
    file, err := os.Open(filename)
    if err != nil {
        return err
    }
    defer file.Close()  // Always closes
    
    // Read file...
    return nil
}

// Defer with function
func example3() {
    x := 1
    defer func() {
        fmt.Println(x)  // Captures x by reference
    }()
    x = 2
}
// Output: 2

// Defer with value
func example4() {
    x := 1
    defer fmt.Println(x)  // Captures value at defer time
    x = 2
}
// Output: 1

// Defer for cleanup
func process() {
    resource := acquireResource()
    defer releaseResource(resource)  // Always releases
    
    // Use resource...
}
```

**Key Points:**
- Executes in reverse order (LIFO)
- Arguments evaluated immediately
- Useful for cleanup (files, locks, etc.)
- Always executes (even with panic/return)

---

## Concurrency

### Q35. What are goroutines? (Medium)

**Answer:**
Goroutines are lightweight threads managed by the Go runtime:

```go
// Starting a goroutine
go functionName()

// Anonymous function
go func() {
    fmt.Println("Running in goroutine")
}()

// With parameters
go func(msg string) {
    fmt.Println(msg)
}("Hello")

// Example
func sayHello(name string) {
    for i := 0; i < 3; i++ {
        fmt.Printf("Hello from %s\n", name)
        time.Sleep(100 * time.Millisecond)
    }
}

func main() {
    go sayHello("Alice")
    go sayHello("Bob")
    time.Sleep(1 * time.Second)  // Wait for goroutines
}

// Goroutine with channel
func worker(id int, jobs <-chan int, results chan<- int) {
    for job := range jobs {
        fmt.Printf("Worker %d processing job %d\n", id, job)
        results <- job * 2
    }
}
```

**Key Points:**
- Very lightweight (thousands can run simultaneously)
- Managed by Go runtime (not OS threads)
- Started with `go` keyword
- Share memory (use channels for communication)

---

### Q36. What are channels in Go? (Medium)

**Answer:**
Channels are typed conduits for communication between goroutines:

```go
// Channel declaration
ch := make(chan int)           // Unbuffered
ch := make(chan int, 10)       // Buffered (capacity 10)

// Sending and receiving
ch <- 42          // Send
value := <-ch     // Receive
value, ok := <-ch // Receive with check (ok is false if closed)

// Closing channels
close(ch)

// Example
func main() {
    ch := make(chan string)
    
    go func() {
        ch <- "Hello"
        ch <- "World"
        close(ch)
    }()
    
    for msg := range ch {
        fmt.Println(msg)
    }
}

// Channel directions
func sendOnly(ch chan<- int) {  // Send-only
    ch <- 42
}

func receiveOnly(ch <-chan int) {  // Receive-only
    value := <-ch
}
```

**Unbuffered vs Buffered:**
- **Unbuffered:** Synchronous (sender blocks until receiver ready)
- **Buffered:** Asynchronous (sender blocks only when buffer full)

---

### Q37. Explain channel buffering. (Medium)

**Answer:**

```go
// Unbuffered channel (synchronous)
unbuffered := make(chan int)
// Sender blocks until receiver is ready
// Receiver blocks until sender is ready

// Buffered channel (asynchronous)
buffered := make(chan int, 3)  // Capacity 3

// Example
func main() {
    ch := make(chan int, 2)  // Buffer size 2
    
    ch <- 1  // Non-blocking (buffer has space)
    ch <- 2  // Non-blocking (buffer has space)
    // ch <- 3  // Would block (buffer full)
    
    fmt.Println(<-ch)  // 1
    fmt.Println(<-ch)  // 2
}

// Producer-consumer with buffered channel
func producer(ch chan<- int) {
    for i := 0; i < 10; i++ {
        ch <- i
        fmt.Printf("Produced: %d\n", i)
    }
    close(ch)
}

func consumer(ch <-chan int) {
    for val := range ch {
        fmt.Printf("Consumed: %d\n", val)
        time.Sleep(100 * time.Millisecond)
    }
}

func main() {
    ch := make(chan int, 5)  // Buffer allows async operation
    go producer(ch)
    consumer(ch)
}
```

**Key Points:**
- Buffered channels allow async communication
- Sender blocks only when buffer is full
- Receiver blocks only when buffer is empty
- Useful for producer-consumer patterns

---

### Q38. What is the select statement? (Medium)

**Answer:**
`select` lets a goroutine wait on multiple channel operations:

```go
// Basic select
select {
case msg1 := <-ch1:
    fmt.Println("Received from ch1:", msg1)
case msg2 := <-ch2:
    fmt.Println("Received from ch2:", msg2)
}

// Select with default (non-blocking)
select {
case msg := <-ch:
    fmt.Println("Received:", msg)
default:
    fmt.Println("No message available")
}

// Select for sending
select {
case ch <- value:
    fmt.Println("Sent:", value)
default:
    fmt.Println("Channel full")
}

// Select with timeout
select {
case msg := <-ch:
    fmt.Println("Received:", msg)
case <-time.After(1 * time.Second):
    fmt.Println("Timeout")
}

// Select with context
select {
case <-ctx.Done():
    fmt.Println("Context cancelled")
case msg := <-ch:
    fmt.Println("Received:", msg)
}

// Multiple cases
for {
    select {
    case msg := <-ch1:
        process(msg)
    case msg := <-ch2:
        process(msg)
    case <-done:
        return
    }
}
```

**Key Points:**
- Chooses one ready case randomly if multiple ready
- Blocks if no case ready (unless `default`)
- Useful for multiplexing channels

---

### Q39. Explain worker pools in Go. (Tough)

**Answer:**
Worker pools use multiple goroutines to process jobs:

```go
func worker(id int, jobs <-chan int, results chan<- int) {
    for job := range jobs {
        fmt.Printf("Worker %d processing job %d\n", id, job)
        time.Sleep(1 * time.Second)  // Simulate work
        results <- job * 2
    }
}

func main() {
    numJobs := 10
    numWorkers := 3
    
    jobs := make(chan int, numJobs)
    results := make(chan int, numJobs)
    
    // Start workers
    for w := 1; w <= numWorkers; w++ {
        go worker(w, jobs, results)
    }
    
    // Send jobs
    for j := 1; j <= numJobs; j++ {
        jobs <- j
    }
    close(jobs)
    
    // Collect results
    for r := 1; r <= numJobs; r++ {
        fmt.Println("Result:", <-results)
    }
}

// Worker pool with error handling
type Job struct {
    ID    int
    Data  string
}

type Result struct {
    Job    Job
    Output string
    Err    error
}

func worker(id int, jobs <-chan Job, results chan<- Result) {
    for job := range jobs {
        result := Result{Job: job}
        // Process job...
        result.Output = fmt.Sprintf("Processed: %s", job.Data)
        results <- result
    }
}
```

**Benefits:**
- Control concurrency level
- Reuse goroutines
- Better resource management

---

### Q40. What are WaitGroups? (Medium)

**Answer:**
`sync.WaitGroup` waits for a collection of goroutines to finish:

```go
import "sync"

func worker(id int, wg *sync.WaitGroup) {
    defer wg.Done()  // Decrement counter when done
    
    fmt.Printf("Worker %d starting\n", id)
    time.Sleep(1 * time.Second)
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup
    
    for i := 1; i <= 3; i++ {
        wg.Add(1)  // Increment counter
        go worker(i, &wg)
    }
    
    wg.Wait()  // Wait for all goroutines to finish
    fmt.Println("All workers done")
}

// Common pattern
func processItems(items []string) {
    var wg sync.WaitGroup
    
    for _, item := range items {
        wg.Add(1)
        go func(it string) {
            defer wg.Done()
            process(it)
        }(item)
    }
    
    wg.Wait()
}
```

**Methods:**
- `Add(delta)`: Increment counter
- `Done()`: Decrement counter (calls `Add(-1)`)
- `Wait()`: Block until counter is 0

---

### Q41. Explain mutexes in Go. (Medium)

**Answer:**
Mutexes provide mutual exclusion for shared resources:

```go
import "sync"

type SafeCounter struct {
    mu    sync.Mutex
    value int
}

func (c *SafeCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.value++
}

func (c *SafeCounter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()
    return c.value
}

// Example
func main() {
    counter := SafeCounter{}
    var wg sync.WaitGroup
    
    for i := 0; i < 1000; i++ {
        wg.Add(1)
        go func() {
            defer wg.Done()
            counter.Increment()
        }()
    }
    
    wg.Wait()
    fmt.Println(counter.Value())  // 1000
}

// RWMutex (read-write mutex)
type SafeMap struct {
    mu sync.RWMutex
    m  map[string]int
}

func (sm *SafeMap) Get(key string) int {
    sm.mu.RLock()  // Read lock
    defer sm.mu.RUnlock()
    return sm.m[key]
}

func (sm *SafeMap) Set(key string, value int) {
    sm.mu.Lock()  // Write lock
    defer sm.mu.Unlock()
    sm.m[key] = value
}
```

**Key Points:**
- `Lock()`/`Unlock()`: Exclusive access
- `RLock()`/`RUnlock()`: Shared read access (RWMutex)
- Always use `defer` to ensure unlock
- Prefer channels for communication, mutexes for shared state

---

### Q42. What is context in Go? (Tough)

**Answer:**
`context.Context` carries deadlines, cancellation signals, and values:

```go
import "context"

// Background context
ctx := context.Background()

// With timeout
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

// With deadline
deadline := time.Now().Add(10 * time.Second)
ctx, cancel := context.WithDeadline(context.Background(), deadline)
defer cancel()

// With cancellation
ctx, cancel := context.WithCancel(context.Background())
defer cancel()

// With value
ctx := context.WithValue(context.Background(), "userID", "123")

// Checking context
func process(ctx context.Context) error {
    select {
    case <-ctx.Done():
        return ctx.Err()  // context.Canceled or context.DeadlineExceeded
    case <-time.After(2 * time.Second):
        return nil
    }
}

// HTTP request with context
func makeRequest(ctx context.Context, url string) error {
    req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        return err
    }
    defer resp.Body.Close()
    return nil
}

// Passing context through call chain
func handler(ctx context.Context) error {
    return service(ctx)
}

func service(ctx context.Context) error {
    return repository(ctx)
}
```

**Use Cases:**
- Request cancellation
- Timeouts
- Passing request-scoped values
- Graceful shutdown

---

## String Operations

### Q43. How do you work with strings in Go? (Easy)

**Answer:**

```go
// String basics
s := "Hello, World"
length := len(s)  // Byte length, not rune length

// String concatenation
s1 := "Hello"
s2 := "World"
s3 := s1 + ", " + s2
s4 := fmt.Sprintf("%s, %s", s1, s2)

// Strings package
import "strings"

strings.Contains(s, "World")        // true
strings.HasPrefix(s, "Hello")       // true
strings.HasSuffix(s, "World")       // true
strings.Index(s, "World")           // 7
strings.Replace(s, "World", "Go", -1)
strings.ToUpper(s)                  // "HELLO, WORLD"
strings.ToLower(s)                  // "hello, world"
strings.TrimSpace("  hello  ")      // "hello"
strings.Split(s, ",")               // []string{"Hello", " World"}
strings.Join([]string{"a", "b"}, ",")  // "a,b"

// String formatting
import "fmt"

fmt.Sprintf("Name: %s, Age: %d", "Alice", 30)
fmt.Printf("Value: %v\n", value)
```

---

### Q44. What are runes in Go? (Medium)

**Answer:**
Runes are Unicode code points (int32):

```go
// Rune is alias for int32
var r rune = 'A'
var r2 rune = '世'

// String to runes
s := "Hello, 世界"
runes := []rune(s)

// Runes to string
runes := []rune{'H', 'e', 'l', 'l', 'o'}
s := string(runes)

// Iterating over string (by runes)
s := "Hello, 世界"
for i, r := range s {
    fmt.Printf("Index: %d, Rune: %c\n", i, r)
}

// Rune count
s := "Hello, 世界"
runeCount := len([]rune(s))  // 9 (not byte length)

// Unicode package
import "unicode"

unicode.IsLetter('A')    // true
unicode.IsDigit('5')     // true
unicode.IsSpace(' ')     // true
unicode.ToUpper('a')     // 'A'
unicode.ToLower('A')     // 'a'
```

**Key Points:**
- Go strings are UTF-8 encoded
- `len(string)` returns byte length, not character count
- Use `[]rune` for character-level operations

---

## File Operations

### Q45. How do you read files in Go? (Medium)

**Answer:**

```go
import (
    "io/ioutil"  // Deprecated in Go 1.16+, use os.ReadFile
    "os"
    "bufio"
)

// 1. Read entire file (Go 1.16+)
data, err := os.ReadFile("file.txt")
if err != nil {
    log.Fatal(err)
}
content := string(data)

// 2. Read file line by line
file, err := os.Open("file.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

scanner := bufio.NewScanner(file)
for scanner.Scan() {
    line := scanner.Text()
    fmt.Println(line)
}

if err := scanner.Err(); err != nil {
    log.Fatal(err)
}

// 3. Read with buffer
file, err := os.Open("file.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

buffer := make([]byte, 1024)
for {
    n, err := file.Read(buffer)
    if err == io.EOF {
        break
    }
    if err != nil {
        log.Fatal(err)
    }
    fmt.Print(string(buffer[:n]))
}

// 4. Read all (deprecated, but still works)
data, err := ioutil.ReadFile("file.txt")
```

---

### Q46. How do you write files in Go? (Medium)

**Answer:**

```go
import (
    "os"
    "bufio"
    "fmt"
)

// 1. Write entire file (Go 1.16+)
content := "Hello, World!"
err := os.WriteFile("output.txt", []byte(content), 0644)
if err != nil {
    log.Fatal(err)
}

// 2. Write with file handle
file, err := os.Create("output.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

file.WriteString("Hello, World!\n")
file.Write([]byte("More content\n"))

// 3. Buffered writing
file, err := os.Create("output.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

writer := bufio.NewWriter(file)
writer.WriteString("Line 1\n")
writer.WriteString("Line 2\n")
writer.Flush()  // Don't forget to flush!

// 4. Append to file
file, err := os.OpenFile("output.txt", os.O_APPEND|os.O_WRONLY|os.O_CREATE, 0644)
if err != nil {
    log.Fatal(err)
}
defer file.Close()

file.WriteString("Appended line\n")

// 5. Using fmt.Fprintf
file, err := os.Create("output.txt")
if err != nil {
    log.Fatal(err)
}
defer file.Close()

fmt.Fprintf(file, "Name: %s, Age: %d\n", "Alice", 30)
```

---

## JSON and XML

### Q47. How do you work with JSON in Go? (Medium)

**Answer:**

```go
import (
    "encoding/json"
    "fmt"
)

// Struct with JSON tags
type Person struct {
    Name  string `json:"name"`
    Age   int    `json:"age"`
    Email string `json:"email,omitempty"`  // Omit if empty
}

// Marshal (Go to JSON)
person := Person{Name: "Alice", Age: 30}
jsonData, err := json.Marshal(person)
if err != nil {
    log.Fatal(err)
}
fmt.Println(string(jsonData))  // {"name":"Alice","age":30}

// Pretty print
jsonData, _ := json.MarshalIndent(person, "", "  ")

// Unmarshal (JSON to Go)
jsonStr := `{"name":"Bob","age":25}`
var person Person
err := json.Unmarshal([]byte(jsonStr), &person)
if err != nil {
    log.Fatal(err)
}

// Decoder (streaming)
decoder := json.NewDecoder(reader)
var person Person
err := decoder.Decode(&person)

// Encoder (streaming)
encoder := json.NewEncoder(writer)
err := encoder.Encode(person)

// Unknown structure
var data map[string]interface{}
json.Unmarshal(jsonData, &data)
```

---

### Q48. How do you work with XML in Go? (Medium)

**Answer:**

```go
import "encoding/xml"

// Struct with XML tags
type Person struct {
    XMLName xml.Name `xml:"person"`
    Name    string   `xml:"name"`
    Age     int      `xml:"age"`
    Email   string   `xml:"email,attr"`  // Attribute
}

// Marshal
person := Person{Name: "Alice", Age: 30, Email: "alice@example.com"}
xmlData, err := xml.MarshalIndent(person, "", "  ")

// Unmarshal
var person Person
err := xml.Unmarshal(xmlData, &person)

// With XML header
xmlData := []byte(xml.Header + string(data))
```

---

## HTTP Client and Server

### Q49. How do you create an HTTP server in Go? (Medium)

**Answer:**

```go
import (
    "fmt"
    "net/http"
)

// Basic handler
func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

// Handler with path parameters
func userHandler(w http.ResponseWriter, r *http.Request) {
    switch r.Method {
    case "GET":
        fmt.Fprintf(w, "Get user")
    case "POST":
        fmt.Fprintf(w, "Create user")
    default:
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
    }
}

// Handler function type
type HandlerFunc func(http.ResponseWriter, *http.Request)

// ServeMux (router)
mux := http.NewServeMux()
mux.HandleFunc("/", helloHandler)
mux.HandleFunc("/user", userHandler)

// Start server
http.ListenAndServe(":8080", mux)

// With custom server
server := &http.Server{
    Addr:    ":8080",
    Handler: mux,
    ReadTimeout:  15 * time.Second,
    WriteTimeout: 15 * time.Second,
}
server.ListenAndServe()

// JSON response
func jsonHandler(w http.ResponseWriter, r *http.Request) {
    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(map[string]string{"message": "Hello"})
}
```

---

### Q50. How do you make HTTP requests in Go? (Medium)

**Answer:**

```go
import (
    "net/http"
    "io/ioutil"
    "bytes"
    "encoding/json"
)

// GET request
resp, err := http.Get("https://api.example.com/data")
if err != nil {
    log.Fatal(err)
}
defer resp.Body.Close()

body, err := ioutil.ReadAll(resp.Body)

// POST request
data := map[string]string{"name": "Alice"}
jsonData, _ := json.Marshal(data)

resp, err := http.Post("https://api.example.com/users", 
    "application/json", 
    bytes.NewBuffer(jsonData))

// Custom request
req, err := http.NewRequest("GET", "https://api.example.com/data", nil)
req.Header.Set("Authorization", "Bearer token")
req.Header.Set("Content-Type", "application/json")

client := &http.Client{Timeout: 10 * time.Second}
resp, err := client.Do(req)

// With context
ctx := context.Background()
req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
resp, err := client.Do(req)
```

---

## Testing

### Q51. How do you write tests in Go? (Medium)

**Answer:**

```go
// File: math_test.go
package math

import "testing"

// Basic test
func TestAdd(t *testing.T) {
    result := Add(2, 3)
    expected := 5
    if result != expected {
        t.Errorf("Add(2, 3) = %d; expected %d", result, expected)
    }
}

// Table-driven test
func TestMultiply(t *testing.T) {
    tests := []struct {
        a, b     int
        expected int
    }{
        {2, 3, 6},
        {0, 5, 0},
        {-1, 4, -4},
    }
    
    for _, tt := range tests {
        result := Multiply(tt.a, tt.b)
        if result != tt.expected {
            t.Errorf("Multiply(%d, %d) = %d; expected %d", 
                tt.a, tt.b, result, tt.expected)
        }
    }
}

// Benchmark
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(2, 3)
    }
}

// Example (documentation)
func ExampleAdd() {
    result := Add(2, 3)
    fmt.Println(result)
    // Output: 5
}

// Running tests
// go test
// go test -v
// go test -run TestAdd
// go test -bench=.
```

---

### Q52. How do you test HTTP handlers? (Medium)

**Answer:**

```go
import (
    "net/http"
    "net/http/httptest"
    "testing"
)

func TestHandler(t *testing.T) {
    req, _ := http.NewRequest("GET", "/hello", nil)
    w := httptest.NewRecorder()
    
    handler := http.HandlerFunc(helloHandler)
    handler.ServeHTTP(w, req)
    
    if w.Code != http.StatusOK {
        t.Errorf("Expected status 200, got %d", w.Code)
    }
    
    expected := "Hello, World!"
    if w.Body.String() != expected {
        t.Errorf("Expected %s, got %s", expected, w.Body.String())
    }
}

// Testing JSON response
func TestJSONHandler(t *testing.T) {
    req, _ := http.NewRequest("GET", "/api/user", nil)
    w := httptest.NewRecorder()
    
    jsonHandler(w, req)
    
    if w.Header().Get("Content-Type") != "application/json" {
        t.Error("Content-Type not set correctly")
    }
}
```

---

## Advanced Topics

### Q53. What are generics in Go? (Tough)

**Answer:**
Generics (Go 1.18+) allow writing code that works with multiple types:

```go
// Generic function
func Swap[T any](a, b T) (T, T) {
    return b, a
}

// Usage
x, y := Swap(1, 2)
s1, s2 := Swap("hello", "world")

// Generic type
type Stack[T any] struct {
    items []T
}

func (s *Stack[T]) Push(item T) {
    s.items = append(s.items, item)
}

func (s *Stack[T]) Pop() T {
    item := s.items[len(s.items)-1]
    s.items = s.items[:len(s.items)-1]
    return item
}

// Usage
stack := Stack[int]{}
stack.Push(1)
stack.Push(2)
value := stack.Pop()

// Type constraints
type Number interface {
    int | float64
}

func Add[T Number](a, b T) T {
    return a + b
}

// Comparable constraint
func Find[T comparable](slice []T, value T) int {
    for i, v := range slice {
        if v == value {
            return i
        }
    }
    return -1
}
```

---

### Q54. Explain packages and modules in Go. (Medium)

**Answer:**

```go
// Package declaration (first line)
package main  // Executable package

package utils  // Library package

// Importing packages
import "fmt"
import "net/http"

// Multiple imports
import (
    "fmt"
    "net/http"
)

// Import with alias
import f "fmt"
f.Println("Hello")

// Import for side effects
import _ "database/sql/driver"

// Modules (go.mod)
// module github.com/user/project
// go 1.18
// require (
//     github.com/gin-gonic/gin v1.9.0
// )

// Creating module
// go mod init github.com/user/project

// Adding dependencies
// go get github.com/gin-gonic/gin

// Private vs Public
// Uppercase = exported (public)
func PublicFunction() {}

// Lowercase = unexported (private)
func privateFunction() {}
```

---

### Q55. How does garbage collection work in Go? (Tough)

**Answer:**
Go uses a concurrent, tri-color mark-and-sweep garbage collector:

**Features:**
- Concurrent (runs alongside program)
- Low latency (short pause times)
- Automatic memory management
- Tuned for low latency over throughput

**How it works:**
1. **Mark phase:** Traces reachable objects (white → gray → black)
2. **Sweep phase:** Frees unreachable objects
3. Runs concurrently with program execution

**Tuning:**
```go
// Set GC percentage (default 100)
debug.SetGCPercent(50)  // More aggressive GC

// Force GC
runtime.GC()

// Memory stats
var m runtime.MemStats
runtime.ReadMemStats(&m)
fmt.Printf("Heap: %d KB\n", m.Alloc/1024)
```

**Best Practices:**
- Avoid unnecessary allocations
- Reuse buffers/slices
- Use object pools for frequently allocated objects
- Profile memory usage

---

### Q56. What is the difference between `make` and `new`? (Medium)

**Answer:**

```go
// new: Allocates memory, returns pointer, zero-initialized
p := new(int)        // *int pointing to 0
p2 := new([5]int)    // *[5]int (array of zeros)

// make: Allocates and initializes slices, maps, channels
s := make([]int, 5)           // Slice with length 5
m := make(map[string]int)     // Empty map
ch := make(chan int, 10)      // Buffered channel

// Differences
// new: Returns pointer, works with any type, zero value
// make: Returns value (not pointer), only for slice/map/channel, initialized

// Equivalent operations
p1 := new(int)
var p2 *int = new(int)

s1 := make([]int, 5)
var s2 []int = make([]int, 5)
```

**When to use:**
- `new`: When you need a pointer to zero value
- `make`: When creating slices, maps, or channels

---

### Q57. Explain the init function in Go. (Medium)

**Answer:**
`init` functions run automatically before `main`:

```go
package main

import "fmt"

var globalVar = initGlobal()

func initGlobal() int {
    fmt.Println("Initializing global variable")
    return 42
}

func init() {
    fmt.Println("Init function 1")
}

func init() {
    fmt.Println("Init function 2")
}

func main() {
    fmt.Println("Main function")
}

// Output:
// Initializing global variable
// Init function 1
// Init function 2
// Main function
```

**Key Points:**
- Runs automatically
- Multiple `init` functions allowed (executed in order)
- Runs after package variables initialized
- Runs before `main`
- Used for package initialization

---

### Q58. How do you handle time in Go? (Medium)

**Answer:**

```go
import "time"

// Current time
now := time.Now()

// Creating time
t := time.Date(2024, 1, 15, 10, 30, 0, 0, time.UTC)

// Parsing time
t, err := time.Parse("2006-01-02", "2024-01-15")
t, err := time.Parse(time.RFC3339, "2024-01-15T10:30:00Z")

// Formatting time
formatted := now.Format("2006-01-02 15:04:05")
formatted := now.Format(time.RFC3339)

// Time operations
future := now.Add(24 * time.Hour)
past := now.Add(-1 * time.Hour)
duration := future.Sub(now)

// Sleep
time.Sleep(1 * time.Second)

// Timer
timer := time.NewTimer(5 * time.Second)
<-timer.C

// Ticker
ticker := time.NewTicker(1 * time.Second)
for t := range ticker.C {
    fmt.Println("Tick at", t)
}

// Epoch
epoch := time.Unix(1705315200, 0)
unix := now.Unix()
```

**Reference Time:** `Mon Jan 2 15:04:05 MST 2006` (01/02 03:04:05PM '06 -0700)

---

### Q59. How do you work with environment variables? (Easy)

**Answer:**

```go
import "os"

// Get environment variable
value := os.Getenv("HOME")
value, exists := os.LookupEnv("HOME")  // Check if exists

// Set environment variable
os.Setenv("KEY", "value")

// All environment variables
env := os.Environ()
for _, e := range env {
    fmt.Println(e)  // KEY=value format
}

// Common pattern
port := os.Getenv("PORT")
if port == "" {
    port = "8080"  // Default
}
```

---

### Q60. Explain command-line arguments and flags. (Medium)

**Answer:**

```go
import (
    "flag"
    "os"
)

// Basic arguments
args := os.Args
// os.Args[0] is program name
// os.Args[1:] are arguments

// Using flag package
name := flag.String("name", "Guest", "Name to greet")
age := flag.Int("age", 0, "Age")
verbose := flag.Bool("verbose", false, "Verbose output")

flag.Parse()

fmt.Printf("Hello, %s! Age: %d\n", *name, *age)
if *verbose {
    fmt.Println("Verbose mode enabled")
}

// Usage: go run main.go -name=Alice -age=30 -verbose

// Custom flag
var customVar string
flag.StringVar(&customVar, "custom", "default", "Custom variable")

// Subcommands
var cmd = flag.NewFlagSet("cmd", flag.ExitOnError)
var subFlag = cmd.String("flag", "default", "Subcommand flag")

if len(os.Args) < 2 {
    fmt.Println("Expected subcommand")
    os.Exit(1)
}

switch os.Args[1] {
case "subcommand":
    cmd.Parse(os.Args[2:])
    fmt.Println("Flag:", *subFlag)
default:
    fmt.Println("Unknown command")
}
```

---

## Summary

This document covers essential Go (Golang) interview topics from basic syntax to advanced concurrency patterns. Key areas include:

- **Fundamentals:** Variables, types, control flow
- **Data Structures:** Arrays, slices, maps
- **Functions:** Variadic, closures, recursion
- **Concurrency:** Goroutines, channels, select, worker pools
- **Error Handling:** Errors, panic, recover, defer
- **Advanced:** Generics, interfaces, reflection
- **Practical:** HTTP, JSON, file I/O, testing

**Difficulty Levels:**
- **Easy:** Basic syntax, concepts, simple operations
- **Medium:** Common patterns, concurrency basics, standard library
- **Tough:** Advanced concurrency, generics, performance optimization

---

## References

- [Go Roadmap](https://roadmap.sh/golang)
- [Go by Example](https://gobyexample.com/)
- [Official Go Documentation](https://go.dev/doc/)
- [Effective Go](https://go.dev/doc/effective_go)

---

*Last Updated: 2024*

