# Go Programming Language Concepts

> Comprehensive guide to Go concepts based on [Go by Example](https://gobyexample.com/)

---

## Table of Contents

1. [Hello World](#hello-world)
2. [Values](#values)
3. [Variables](#variables)
4. [Constants](#constants)
5. [For Loops](#for-loops)
6. [If/Else](#ifelse)
7. [Switch](#switch)
8. [Arrays](#arrays)
9. [Slices](#slices)
10. [Maps](#maps)
11. [Functions](#functions)
12. [Multiple Return Values](#multiple-return-values)
13. [Variadic Functions](#variadic-functions)
14. [Closures](#closures)
15. [Recursion](#recursion)
16. [Range over Built-in Types](#range-over-built-in-types)
17. [Pointers](#pointers)
18. [Strings and Runes](#strings-and-runes)
19. [Structs](#structs)
20. [Methods](#methods)
21. [Interfaces](#interfaces)
22. [Enums](#enums)
23. [Struct Embedding](#struct-embedding)
24. [Generics](#generics)
25. [Range over Iterators](#range-over-iterators)
26. [Errors](#errors)
27. [Custom Errors](#custom-errors)
28. [Goroutines](#goroutines)
29. [Channels](#channels)
30. [Channel Buffering](#channel-buffering)
31. [Channel Synchronization](#channel-synchronization)
32. [Channel Directions](#channel-directions)
33. [Select](#select)
34. [Timeouts](#timeouts)
35. [Non-Blocking Channel Operations](#non-blocking-channel-operations)
36. [Closing Channels](#closing-channels)
37. [Range over Channels](#range-over-channels)
38. [Timers](#timers)
39. [Tickers](#tickers)
40. [Worker Pools](#worker-pools)
41. [WaitGroups](#waitgroups)
42. [Rate Limiting](#rate-limiting)
43. [Atomic Counters](#atomic-counters)
44. [Mutexes](#mutexes)
45. [Stateful Goroutines](#stateful-goroutines)
46. [Sorting](#sorting)
47. [Sorting by Functions](#sorting-by-functions)
48. [Panic](#panic)
49. [Defer](#defer)
50. [Recover](#recover)
51. [String Functions](#string-functions)
52. [String Formatting](#string-formatting)
53. [Text Templates](#text-templates)
54. [Regular Expressions](#regular-expressions)
55. [JSON](#json)
56. [XML](#xml)
57. [Time](#time)
58. [Epoch](#epoch)
59. [Time Formatting / Parsing](#time-formatting--parsing)
60. [Random Numbers](#random-numbers)
61. [Number Parsing](#number-parsing)
62. [URL Parsing](#url-parsing)
63. [SHA256 Hashes](#sha256-hashes)
64. [Base64 Encoding](#base64-encoding)
65. [Reading Files](#reading-files)
66. [Writing Files](#writing-files)
67. [Line Filters](#line-filters)
68. [File Paths](#file-paths)
69. [Directories](#directories)
70. [Temporary Files and Directories](#temporary-files-and-directories)
71. [Embed Directive](#embed-directive)
72. [Testing and Benchmarking](#testing-and-benchmarking)
73. [Command-Line Arguments](#command-line-arguments)
74. [Command-Line Flags](#command-line-flags)
75. [Command-Line Subcommands](#command-line-subcommands)
76. [Environment Variables](#environment-variables)
77. [Logging](#logging)
78. [HTTP Client](#http-client)
79. [HTTP Server](#http-server)
80. [TCP Server](#tcp-server)
81. [Context](#context)
82. [Spawning Processes](#spawning-processes)
83. [Exec'ing Processes](#execing-processes)
84. [Signals](#signals)
85. [Exit](#exit)

---

## Hello World

Every Go program starts with a `main` package and a `main` function. This is the simplest Go program.

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

**Explanation:**
- `package main` declares this as the main package (entry point of the program)
- `import "fmt"` imports the format package for I/O operations
- `func main()` is the entry point function that gets executed
- `fmt.Println()` prints text to standard output

---

## Values

Go has various value types including strings, integers, floats, and booleans.

```go
package main

import "fmt"

func main() {
    // Strings
    fmt.Println("go" + "lang")
    
    // Integers
    fmt.Println("1+1 =", 1+1)
    fmt.Println("7.0/3.0 =", 7.0/3.0)
    
    // Booleans
    fmt.Println(true && false)
    fmt.Println(true || false)
    fmt.Println(!true)
}
```

**Output:**
```
golang
1+1 = 2
7.0/3.0 = 2.3333333333333335
false
true
false
```

**Key Points:**
- String concatenation uses `+`
- Go performs type inference for numeric operations
- Boolean operators: `&&` (AND), `||` (OR), `!` (NOT)

---

## Variables

Variables in Go are explicitly declared and used by the compiler to ensure type correctness.

```go
package main

import "fmt"

func main() {
    // Declare a single variable
    var a = "initial"
    fmt.Println(a)

    // Declare multiple variables
    var b, c int = 1, 2
    fmt.Println(b, c)

    // Go infers the type of initialized variables
    var d = true
    fmt.Println(d)

    // Variables declared without initialization are zero-valued
    var e int
    fmt.Println(e)

    // Short variable declaration (only inside functions)
    f := "apple"
    fmt.Println(f)
}
```

**Explanation:**
- `var` keyword declares variables
- Variables can be declared with or without explicit types
- Uninitialized variables get their zero value (0 for numbers, false for bool, "" for strings)
- `:=` is shorthand for declaring and initializing (only inside functions)
- Multiple variables can be declared in one statement

**Zero Values:**
- `int`: 0
- `float64`: 0.0
- `bool`: false
- `string`: ""
- Pointers, slices, maps, channels: `nil`

---

## Constants

Constants are declared using the `const` keyword and cannot be changed after declaration.

```go
package main

import (
    "fmt"
    "math"
)

const s string = "constant"

func main() {
    fmt.Println(s)

    const n = 500000000

    // Constant expressions perform arithmetic with arbitrary precision
    const d = 3e20 / n
    fmt.Println(d)

    // A numeric constant has no type until it's given one
    fmt.Println(int64(d))

    // A number can be given a type by using it in a context that requires one
    fmt.Println(math.Sin(n))
}
```

**Key Points:**
- Constants can be character, string, boolean, or numeric values
- Numeric constants are high-precision values
- An untyped constant takes the type needed by its context
- Constants cannot be declared using `:=` syntax

---


## For Loops

Go has only one looping construct: the `for` loop. It can be used in multiple forms.

```go
package main

import "fmt"

func main() {
    // Classic for loop
    for i := 0; i < 3; i++ {
        fmt.Println(i)
    }

    // For loop as a while loop
    j := 0
    for j < 3 {
        fmt.Println(j)
        j++
    }

    // Infinite loop with break
    for {
        fmt.Println("loop")
        break
    }

    // Continue to next iteration
    for n := 0; n <= 5; n++ {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
}
```

**Key Points:**
- Go's `for` loop has three components: init statement, condition, post statement
- The init and post statements are optional
- `for` can be used as a `while` loop
- `break` exits the loop
- `continue` skips to the next iteration

---

## If/Else

Go's `if` statements are straightforward and can include an optional initialization statement.

```go
package main

import "fmt"

func main() {
    if 7%2 == 0 {
        fmt.Println("7 is even")
    } else {
        fmt.Println("7 is odd")
    }

    if 8%4 == 0 {
        fmt.Println("8 is divisible by 4")
    }

    // If with a short statement
    if num := 9; num < 0 {
        fmt.Println(num, "is negative")
    } else if num < 10 {
        fmt.Println(num, "has 1 digit")
    } else {
        fmt.Println(num, "has multiple digits")
    }
}
```

**Key Points:**
- No parentheses around conditions (unlike C/Java)
- Braces are required
- Can include a short statement before the condition
- Variables declared in the `if` statement are only available in that scope

---

## Switch

Go's `switch` statement is more flexible than in other languages. It can work without an expression and supports multiple values per case.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    i := 2
    fmt.Print("Write ", i, " as ")
    switch i {
    case 1:
        fmt.Println("one")
    case 2:
        fmt.Println("two")
    case 3:
        fmt.Println("three")
    }

    switch time.Now().Weekday() {
    case time.Saturday, time.Sunday:
        fmt.Println("It's the weekend")
    default:
        fmt.Println("It's a weekday")
    }

    t := time.Now()
    switch {
    case t.Hour() < 12:
        fmt.Println("It's before noon")
    default:
        fmt.Println("It's after noon")
    }

    // Type switch
    whatAmI := func(i interface{}) {
        switch t := i.(type) {
        case bool:
            fmt.Println("I'm a bool")
        case int:
            fmt.Println("I'm an int")
        default:
            fmt.Printf("Don't know type %T\n", t)
        }
    }
    whatAmI(true)
    whatAmI(1)
    whatAmI("hey")
}
```

**Key Points:**
- Cases don't fall through by default (no `break` needed)
- Multiple values can be listed in a case
- Can switch without an expression (like if/else chain)
- Type switches allow checking interface{} types
- `default` case is optional

---

## Arrays

Arrays in Go have a fixed size and specific type. They are rarely used directly; slices are preferred.

```go
package main

import "fmt"

func main() {
    var a [5]int
    fmt.Println("emp:", a)

    a[4] = 100
    fmt.Println("set:", a)
    fmt.Println("get:", a[4])

    fmt.Println("len:", len(a))

    b := [5]int{1, 2, 3, 4, 5}
    fmt.Println("dcl:", b)

    var twoD [2][3]int
    for i := 0; i < 2; i++ {
        for j := 0; j < 3; j++ {
            twoD[i][j] = i + j
        }
    }
    fmt.Println("2d: ", twoD)
}
```

**Key Points:**
- Arrays have a fixed size that must be known at compile time
- Array type includes size: `[5]int` is different from `[10]int`
- Zero-valued arrays have all elements set to zero value
- Arrays are value types (copied when assigned)

---

## Slices

Slices are more flexible than arrays and are used extensively in Go. They are references to underlying arrays.

```go
package main

import "fmt"

func main() {
    s := make([]string, 3)
    fmt.Println("emp:", s)

    s[0] = "a"
    s[1] = "b"
    s[2] = "c"
    fmt.Println("set:", s)
    fmt.Println("get:", s[2])

    fmt.Println("len:", len(s))

    s = append(s, "d")
    s = append(s, "e", "f")
    fmt.Println("apd:", s)

    c := make([]string, len(s))
    copy(c, s)
    fmt.Println("cpy:", c)

    l := s[2:5]
    fmt.Println("sl1:", l)

    l = s[:5]
    fmt.Println("sl2:", l)

    l = s[2:]
    fmt.Println("sl3:", l)

    t := []string{"g", "h", "i"}
    fmt.Println("dcl:", t)

    twoD := make([][]int, 3)
    for i := 0; i < 3; i++ {
        innerLen := i + 1
        twoD[i] = make([]int, innerLen)
        for j := 0; j < innerLen; j++ {
            twoD[i][j] = i + j
        }
    }
    fmt.Println("2d: ", twoD)
}
```

**Key Points:**
- Slices are dynamic and can grow/shrink
- Created with `make([]type, length, capacity)`
- `append()` adds elements and may create a new underlying array
- Slicing syntax: `s[low:high]` creates a new slice
- Slices are reference types (point to underlying array)

---

## Maps

Maps are Go's built-in associative data type (hash tables or dictionaries).

```go
package main

import "fmt"

func main() {
    m := make(map[string]int)

    m["k1"] = 7
    m["k2"] = 13

    fmt.Println("map:", m)

    v1 := m["k1"]
    fmt.Println("v1:", v1)

    fmt.Println("len:", len(m))

    delete(m, "k2")
    fmt.Println("map:", m)

    _, prs := m["k2"]
    fmt.Println("prs:", prs)

    n := map[string]int{"foo": 1, "bar": 2}
    fmt.Println("map:", n)
}
```

**Key Points:**
- Maps are unordered collections of key-value pairs
- Created with `make(map[keyType]valueType)`
- Zero value of a map is `nil` (cannot add keys to nil map)
- Two-value assignment checks if key exists: `val, ok := m["key"]`
- `delete(map, key)` removes a key-value pair

---

## Functions

Functions in Go are defined using the `func` keyword.

```go
package main

import "fmt"

func plus(a int, b int) int {
    return a + b
}

func plusPlus(a, b, c int) int {
    return a + b + c
}

func main() {
    res := plus(1, 2)
    fmt.Println("1+2 =", res)

    res = plusPlus(1, 2, 3)
    fmt.Println("1+2+3 =", res)
}
```

**Key Points:**
- Functions are first-class citizens in Go
- Parameters of the same type can share type declaration
- Functions can be assigned to variables
- Functions can be passed as arguments and returned as values

---

## Multiple Return Values

Go functions can return multiple values, which is commonly used for returning a result and an error.

```go
package main

import "fmt"

func vals() (int, int) {
    return 3, 7
}

func main() {
    a, b := vals()
    fmt.Println(a)
    fmt.Println(b)

    _, c := vals()
    fmt.Println(c)
}
```

**Key Points:**
- Multiple return values are common in Go
- Use `_` to ignore return values
- Often used for returning (result, error) pairs
- Named return values can be used for documentation

---

## Variadic Functions

Variadic functions can be called with any number of trailing arguments.

```go
package main

import "fmt"

func sum(nums ...int) {
    fmt.Print(nums, " ")
    total := 0
    for _, num := range nums {
        total += num
    }
    fmt.Println(total)
}

func main() {
    sum(1, 2)
    sum(1, 2, 3)

    nums := []int{1, 2, 3, 4}
    sum(nums...)
}
```

**Key Points:**
- Use `...` before the type to indicate variadic parameters
- Variadic parameters are treated as a slice inside the function
- Can pass a slice using `slice...` syntax
- Variadic parameter must be the last parameter

---

## Closures

Go supports anonymous functions, which can form closures. Closures are functions that reference variables from outside their body.

```go
package main

import "fmt"

func intSeq() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}

func main() {
    nextInt := intSeq()

    fmt.Println(nextInt())
    fmt.Println(nextInt())
    fmt.Println(nextInt())

    newInts := intSeq()
    fmt.Println(newInts())
}
```

**Output:**
```
1
2
3
1
```

**Key Points:**
- Anonymous functions can access variables from enclosing scope
- Each closure has its own independent variables
- Useful for creating function generators
- Commonly used with goroutines

---

## Recursion

Go supports recursive functions. Here's a classic factorial example.

```go
package main

import "fmt"

func fact(n int) int {
    if n == 0 {
        return 1
    }
    return n * fact(n-1)
}

func main() {
    fmt.Println(fact(7))
}
```

**Output:**
```
5040
```

**Key Points:**
- Recursive functions call themselves
- Must have a base case to prevent infinite recursion
- Go doesn't optimize tail recursion
- Useful for tree/graph traversal, divide-and-conquer algorithms

---

## Range over Built-in Types

The `range` form of the `for` loop iterates over slices, maps, strings, and channels.

```go
package main

import "fmt"

func main() {
    // Range over slice
    nums := []int{2, 3, 4}
    sum := 0
    for _, num := range nums {
        sum += num
    }
    fmt.Println("sum:", sum)

    for i, num := range nums {
        if num == 3 {
            fmt.Println("index:", i)
        }
    }

    // Range over map
    kvs := map[string]string{"a": "apple", "b": "banana"}
    for k, v := range kvs {
        fmt.Printf("%s -> %s\n", k, v)
    }

    // Range over string (gives runes)
    for i, c := range "go" {
        fmt.Println(i, c)
    }
}
```

**Key Points:**
- `range` returns index/key and value
- Use `_` to ignore index/key
- For maps, iteration order is random
- For strings, `range` iterates over Unicode code points (runes)

---

## Pointers

Go supports pointers, allowing you to pass references to values and records.

```go
package main

import "fmt"

func main() {
    i := 42
    p := &i         // Point to i
    fmt.Println(*p) // Read i through the pointer
    *p = 21         // Set i through the pointer
    fmt.Println(i)  // See the new value of i

    j := 2701
    p = &j
    *p = *p / 37
    fmt.Println(j)
}
```

**Key Points:**
- `&` operator generates a pointer to its operand
- `*` operator dereferences a pointer
- No pointer arithmetic (unlike C)
- Pointers are useful for passing large structs efficiently
- Zero value of pointer is `nil`

---

## Strings and Runes

A string in Go is a read-only slice of bytes. A `rune` is an alias for `int32` and represents a Unicode code point.

```go
package main

import (
    "fmt"
    "unicode/utf8"
)

func main() {
    const s = "สวัสดี"

    fmt.Println("Len:", len(s))

    for i := 0; i < len(s); i++ {
        fmt.Printf("%x ", s[i])
    }
    fmt.Println()

    fmt.Println("Rune count:", utf8.RuneCountInString(s))

    for idx, runeValue := range s {
        fmt.Printf("%#U starts at %d\n", runeValue, idx)
    }
}
```

**Key Points:**
- Strings are immutable byte slices
- `len(string)` returns bytes, not characters
- Use `utf8.RuneCountInString()` for character count
- `range` over string iterates over runes, not bytes
- Rune is Go's term for Unicode code point

---

## Structs

Structs are typed collections of fields. They're useful for grouping data together.

```go
package main

import "fmt"

type person struct {
    name string
    age  int
}

func main() {
    fmt.Println(person{"Bob", 20})
    fmt.Println(person{name: "Alice", age: 30})
    fmt.Println(person{name: "Fred"})
    fmt.Println(&person{name: "Ann", age: 40})

    s := person{name: "Sean", age: 50}
    fmt.Println(s.name)

    sp := &s
    fmt.Println(sp.age)

    sp.age = 51
    fmt.Println(sp.age)
}
```

**Key Points:**
- Structs group related data together
- Fields can be accessed with dot notation
- Can create struct literals with or without field names
- Pointers to structs can access fields directly (no `->` needed)
- Structs are value types (copied when assigned)

---

## Methods

Go supports methods defined on struct types. Methods are functions with a special receiver argument.

```go
package main

import (
    "fmt"
    "math"
)

type rect struct {
    width, height float64
}

func (r rect) area() float64 {
    return r.width * r.height
}

func (r *rect) perim() float64 {
    return 2*r.width + 2*r.height
}

func main() {
    r := rect{width: 10, height: 5}

    fmt.Println("area: ", r.area())
    fmt.Println("perim:", r.perim())

    rp := &r
    fmt.Println("area: ", rp.area())
    fmt.Println("perim:", rp.perim())
}
```

**Key Points:**
- Methods have a receiver argument before the function name
- Value receiver: `func (r rect) method()`
- Pointer receiver: `func (r *rect) method()`
- Pointer receivers can modify the struct
- Go automatically handles value/pointer conversions

---

## Interfaces

Interfaces are named collections of method signatures. A type implements an interface by implementing its methods.

```go
package main

import (
    "fmt"
    "math"
)

type geometry interface {
    area() float64
    perim() float64
}

type rect struct {
    width, height float64
}

func (r rect) area() float64 {
    return r.width * r.height
}

func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

type circle struct {
    radius float64
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}

func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}

func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}

func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}

    measure(r)
    measure(c)
}
```

**Key Points:**
- Interfaces define behavior, not data
- Types implement interfaces implicitly (duck typing)
- Empty interface `interface{}` can hold any type
- Interface values contain a value and a concrete type
- Interface satisfaction is checked at compile time

---

## Enums

Go doesn't have built-in enums, but they can be implemented using constants and `iota`.

```go
package main

import "fmt"

type ServerState int

const (
    StateIdle ServerState = iota
    StateConnected
    StateError
    StateRetrying
)

func (s ServerState) String() string {
    return [...]string{"Idle", "Connected", "Error", "Retrying"}[s]
}

func main() {
    state := StateConnected
    fmt.Println(state)
}
```

**Key Points:**
- `iota` is a predeclared identifier that represents successive integer constants
- `iota` starts at 0 and increments by 1 for each constant
- Can be used to create enum-like types
- Implementing `String()` method provides readable output

---

## Struct Embedding

Go supports embedding structs and interfaces to express composition.

```go
package main

import "fmt"

type base struct {
    num int
}

func (b base) describe() string {
    return fmt.Sprintf("base with num=%v", b.num)
}

type container struct {
    base
    str string
}

func main() {
    co := container{
        base: base{
            num: 1,
        },
        str: "some name",
    }

    fmt.Printf("co={num: %v, str: %v}\n", co.num, co.str)
    fmt.Println("also num:", co.base.num)
    fmt.Println("describe:", co.describe())

    type describer interface {
        describe() string
    }

    var d describer = co
    fmt.Println("describer:", d.describe())
}
```

**Key Points:**
- Embedded structs allow composition over inheritance
- Methods of embedded struct are promoted to outer struct
- Can access embedded fields directly
- Interfaces can be embedded too

---

## Generics

Go 1.18 introduced generics (type parameters) for writing reusable code.

```go
package main

import "fmt"

func MapKeys[K comparable, V any](m map[K]V) []K {
    r := make([]K, 0, len(m))
    for k := range m {
        r = append(r, k)
    }
    return r
}

type List[T any] struct {
    head, tail *element[T]
}

type element[T any] struct {
    next *element[T]
    val  T
}

func (lst *List[T]) Push(v T) {
    if lst.tail == nil {
        lst.head = &element[T]{val: v}
        lst.tail = lst.head
    } else {
        lst.tail.next = &element[T]{val: v}
        lst.tail = lst.tail.next
    }
}

func (lst *List[T]) GetAll() []T {
    var elems []T
    for e := lst.head; e != nil; e = e.next {
        elems = append(elems, e.val)
    }
    return elems
}

func main() {
    var m = map[int]string{1: "2", 2: "4", 4: "8"}
    fmt.Println("keys:", MapKeys(m))

    _ = MapKeys[int, string](m)

    lst := List[int]{}
    lst.Push(10)
    lst.Push(13)
    lst.Push(23)
    fmt.Println("list:", lst.GetAll())
}
```

**Key Points:**
- Generics allow writing code that works with multiple types
- Syntax: `func Name[T constraint](args) returnType`
- `comparable` constraint for types that can be compared
- `any` is an alias for `interface{}`
- Type parameters can be inferred from function arguments

---

## Range over Iterators

Go 1.23 introduced range over functions (iterators).

```go
package main

import (
    "fmt"
    "iter"
)

func count(start, end int) iter.Seq[int] {
    return func(yield func(int) bool) {
        for i := start; i < end; i++ {
            if !yield(i) {
                return
            }
        }
    }
}

func main() {
    for v := range count(1, 5) {
        fmt.Println(v)
    }
}
```

**Key Points:**
- Iterators allow custom iteration patterns
- Use `iter.Seq[T]` for iterator functions
- Iterator functions take a `yield` function
- Return `false` from yield to stop iteration
- More efficient than returning slices for large datasets

---

## Errors

Errors in Go are values. Functions often return an error as the last return value.

```go
package main

import (
    "errors"
    "fmt"
)

func f1(arg int) (int, error) {
    if arg == 42 {
        return -1, errors.New("can't work with 42")
    }
    return arg + 3, nil
}

func main() {
    for _, i := range []int{7, 42} {
        if r, e := f1(i); e != nil {
            fmt.Println("f1 failed:", e)
        } else {
            fmt.Println("f1 worked:", r)
        }
    }
}
```

**Key Points:**
- Errors are values, not exceptions
- Convention: return `(result, error)` pairs
- `nil` error means success
- Always check errors explicitly
- `errors.New()` creates simple error values

---

## Custom Errors

You can create custom error types by implementing the `error` interface.

```go
package main

import (
    "fmt"
    "time"
)

type MyError struct {
    When time.Time
    What string
}

func (e *MyError) Error() string {
    return fmt.Sprintf("at %v, %s", e.When, e.What)
}

func run() error {
    return &MyError{
        time.Now(),
        "it didn't work",
    }
}

func main() {
    if err := run(); err != nil {
        fmt.Println(err)
    }
}
```

**Key Points:**
- Custom errors implement the `error` interface
- `error` interface: `type error interface { Error() string }`
- Can include additional context (time, stack trace, etc.)
- Use type assertions to check for specific error types

---

## Goroutines

A goroutine is a lightweight thread managed by the Go runtime.

```go
package main

import (
    "fmt"
    "time"
)

func f(from string) {
    for i := 0; i < 3; i++ {
        fmt.Println(from, ":", i)
    }
}

func main() {
    f("direct")

    go f("goroutine")

    go func(msg string) {
        fmt.Println(msg)
    }("going")

    time.Sleep(time.Second)
    fmt.Println("done")
}
```

**Key Points:**
- Goroutines are lightweight (thousands can run concurrently)
- Started with `go` keyword
- Goroutines run concurrently, not necessarily in parallel
- Main goroutine must wait for other goroutines to complete
- Use channels or sync primitives for coordination

---

## Channels

Channels are typed conduits through which you can send and receive values.

```go
package main

import "fmt"

func main() {
    messages := make(chan string)

    go func() {
        messages <- "ping"
    }()

    msg := <-messages
    fmt.Println(msg)
}
```

**Key Points:**
- Channels are created with `make(chan type)`
- `<-` operator sends/receives values
- By default, sends and receives block until both sides are ready
- Channels provide synchronization and communication
- Zero value of channel is `nil`

---

## Channel Buffering

Channels can be buffered. Sends to a buffered channel block only when the buffer is full.

```go
package main

import "fmt"

func main() {
    messages := make(chan string, 2)

    messages <- "buffered"
    messages <- "channel"

    fmt.Println(<-messages)
    fmt.Println(<-messages)
}
```

**Key Points:**
- Buffered channels: `make(chan type, capacity)`
- Sends block only when buffer is full
- Receives block only when buffer is empty
- Useful for decoupling senders and receivers
- Buffer size should be chosen carefully

---

## Channel Synchronization

Channels can be used to synchronize execution across goroutines.

```go
package main

import (
    "fmt"
    "time"
)

func worker(done chan bool) {
    fmt.Print("working...")
    time.Sleep(time.Second)
    fmt.Println("done")

    done <- true
}

func main() {
    done := make(chan bool, 1)
    go worker(done)

    <-done
}
```

**Key Points:**
- Channels can synchronize goroutines
- Receiving from a channel blocks until a value is sent
- Useful for waiting for goroutines to complete
- Alternative to mutexes for simple synchronization

---

## Channel Directions

When using channels as function parameters, you can specify if a channel is only for sending or receiving.

```go
package main

import "fmt"

func ping(pings chan<- string, msg string) {
    pings <- msg
}

func pong(pings <-chan string, pongs chan<- string) {
    msg := <-pings
    pongs <- msg
}

func main() {
    pings := make(chan string, 1)
    pongs := make(chan string, 1)
    ping(pings, "passed message")
    pong(pings, pongs)
    fmt.Println(<-pongs)
}
```

**Key Points:**
- `chan<-` means send-only channel
- `<-chan` means receive-only channel
- Type system enforces channel direction
- Improves code clarity and prevents misuse

---

## Select

The `select` statement lets a goroutine wait on multiple channel operations.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    c1 := make(chan string)
    c2 := make(chan string)

    go func() {
        time.Sleep(1 * time.Second)
        c1 <- "one"
    }()
    go func() {
        time.Sleep(2 * time.Second)
        c2 <- "two"
    }()

    for i := 0; i < 2; i++ {
        select {
        case msg1 := <-c1:
            fmt.Println("received", msg1)
        case msg2 := <-c2:
            fmt.Println("received", msg2)
        }
    }
}
```

**Key Points:**
- `select` waits on multiple channel operations
- Executes the first case that's ready
- If multiple cases ready, chooses randomly
- `default` case makes select non-blocking
- Useful for timeouts and multiplexing

---

## Timeouts

Timeouts are important for programs that connect to external resources.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    c1 := make(chan string, 1)
    go func() {
        time.Sleep(2 * time.Second)
        c1 <- "result 1"
    }()

    select {
    case res := <-c1:
        fmt.Println(res)
    case <-time.After(1 * time.Second):
        fmt.Println("timeout 1")
    }

    c2 := make(chan string, 1)
    go func() {
        time.Sleep(2 * time.Second)
        c2 <- "result 2"
    }()
    select {
    case res := <-c2:
        fmt.Println(res)
    case <-time.After(3 * time.Second):
        fmt.Println("timeout 2")
    }
}
```

**Key Points:**
- `time.After(duration)` returns a channel that receives after duration
- Useful for implementing timeouts
- Prevents indefinite blocking
- Common pattern in network programming

---

## Non-Blocking Channel Operations

Basic sends and receives on channels are blocking. Use `select` with a `default` case for non-blocking operations.

```go
package main

import "fmt"

func main() {
    messages := make(chan string)
    signals := make(chan bool)

    select {
    case msg := <-messages:
        fmt.Println("received message", msg)
    default:
        fmt.Println("no message received")
    }

    msg := "hi"
    select {
    case messages <- msg:
        fmt.Println("sent message", msg)
    default:
        fmt.Println("no message sent")
    }

    select {
    case msg := <-messages:
        fmt.Println("received message", msg)
    case sig := <-signals:
        fmt.Println("received signal", sig)
    default:
        fmt.Println("no activity")
    }
}
```

**Key Points:**
- `default` case in `select` makes it non-blocking
- Useful for checking if a channel operation would block
- Allows implementing polling patterns
- Common in event loops

---

## Closing Channels

Closing a channel indicates that no more values will be sent on it.

```go
package main

import "fmt"

func main() {
    jobs := make(chan int, 5)
    done := make(chan bool)

    go func() {
        for {
            j, more := <-jobs
            if more {
                fmt.Println("received job", j)
            } else {
                fmt.Println("received all jobs")
                done <- true
                return
            }
        }
    }()

    for j := 1; j <= 3; j++ {
        jobs <- j
        fmt.Println("sent job", j)
    }
    close(jobs)
    fmt.Println("sent all jobs")

    <-done
}
```

**Key Points:**
- `close(channel)` closes a channel
- Receiving from closed channel returns zero value and `false`
- Only sender should close channel
- Closing already-closed channel causes panic
- Useful for signaling completion

---

## Range over Channels

You can use `range` to iterate over values received from a channel.

```go
package main

import "fmt"

func main() {
    queue := make(chan string, 2)
    queue <- "one"
    queue <- "two"
    close(queue)

    for elem := range queue {
        fmt.Println(elem)
    }
}
```

**Key Points:**
- `range` over channel receives values until channel is closed
- Automatically stops when channel is closed
- Cleaner than checking `more` in a loop
- Channel must be closed for range to terminate

---

## Timers

Timers represent a single event in the future.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    timer1 := time.NewTimer(2 * time.Second)

    <-timer1.C
    fmt.Println("Timer 1 fired")

    timer2 := time.NewTimer(time.Second)
    go func() {
        <-timer2.C
        fmt.Println("Timer 2 fired")
    }()
    stop2 := timer2.Stop()
    if stop2 {
        fmt.Println("Timer 2 stopped")
    }

    time.Sleep(2 * time.Second)
}
```

**Key Points:**
- `time.NewTimer(duration)` creates a timer
- Timer's channel `C` receives after duration
- `timer.Stop()` cancels timer before it fires
- Useful for one-time delayed execution

---

## Tickers

Tickers are for when you want to do something repeatedly at regular intervals.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    ticker := time.NewTicker(500 * time.Millisecond)
    done := make(chan bool)

    go func() {
        for {
            select {
            case <-done:
                return
            case t := <-ticker.C:
                fmt.Println("Tick at", t)
            }
        }
    }()

    time.Sleep(1600 * time.Millisecond)
    ticker.Stop()
    done <- true
    fmt.Println("Ticker stopped")
}
```

**Key Points:**
- `time.NewTicker(duration)` creates a ticker
- Ticker's channel `C` receives at regular intervals
- `ticker.Stop()` stops the ticker
- Useful for periodic tasks

---

## Worker Pools

Worker pools are a common pattern for concurrent processing.

```go
package main

import (
    "fmt"
    "time"
)

func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        fmt.Println("worker", id, "started job", j)
        time.Sleep(time.Second)
        fmt.Println("worker", id, "finished job", j)
        results <- j * 2
    }
}

func main() {
    const numJobs = 5
    jobs := make(chan int, numJobs)
    results := make(chan int, numJobs)

    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }

    for j := 1; j <= numJobs; j++ {
        jobs <- j
    }
    close(jobs)

    for a := 1; a <= numJobs; a++ {
        <-results
    }
}
```

**Key Points:**
- Worker pool pattern uses multiple goroutines
- Jobs channel distributes work
- Results channel collects results
- Close jobs channel to signal completion
- Efficient for CPU-bound or I/O-bound tasks

---

## WaitGroups

WaitGroups wait for a collection of goroutines to finish.

```go
package main

import (
    "fmt"
    "sync"
    "time"
)

func worker(id int, wg *sync.WaitGroup) {
    defer wg.Done()

    fmt.Printf("Worker %d starting\n", id)
    time.Sleep(time.Second)
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup

    for i := 1; i <= 5; i++ {
        wg.Add(1)
        go worker(i, &wg)
    }

    wg.Wait()
    fmt.Println("All workers completed")
}
```

**Key Points:**
- `sync.WaitGroup` waits for goroutines to complete
- `wg.Add(n)` increments counter
- `wg.Done()` decrements counter (usually with `defer`)
- `wg.Wait()` blocks until counter is zero
- Useful for waiting for multiple goroutines

---

## Rate Limiting

Rate limiting controls the rate of processing requests.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    requests := make(chan int, 5)
    for i := 1; i <= 5; i++ {
        requests <- i
    }
    close(requests)

    limiter := time.Tick(200 * time.Millisecond)

    for req := range requests {
        <-limiter
        fmt.Println("request", req, time.Now())
    }

    burstyLimiter := make(chan time.Time, 3)

    for i := 0; i < 3; i++ {
        burstyLimiter <- time.Now()
    }

    go func() {
        for t := range time.Tick(200 * time.Millisecond) {
            burstyLimiter <- t
        }
    }()

    burstyRequests := make(chan int, 5)
    for i := 1; i <= 5; i++ {
        burstyRequests <- i
    }
    close(burstyRequests)
    for req := range burstyRequests {
        <-burstyLimiter
        fmt.Println("request", req, time.Now())
    }
}
```

**Key Points:**
- Rate limiting prevents overwhelming systems
- `time.Tick()` provides regular rate limiting
- Bursty limiter allows bursts of requests
- Useful for API clients and servers

---

## Atomic Counters

The `sync/atomic` package provides low-level atomic memory operations.

```go
package main

import (
    "fmt"
    "sync"
    "sync/atomic"
)

func main() {
    var ops uint64

    var wg sync.WaitGroup

    for i := 0; i < 50; i++ {
        wg.Add(1)

        go func() {
            for c := 0; c < 1000; c++ {
                atomic.AddUint64(&ops, 1)
            }
            wg.Done()
        }()
    }

    wg.Wait()

    fmt.Println("ops:", ops)
}
```

**Key Points:**
- Atomic operations are thread-safe
- Faster than mutexes for simple operations
- Limited to specific types (int32, int64, uint32, uint64, uintptr, unsafe.Pointer)
- Useful for counters and flags

---

## Mutexes

Mutexes provide mutual exclusion for shared state.

```go
package main

import (
    "fmt"
    "sync"
)

type Container struct {
    mu       sync.Mutex
    counters map[string]int
}

func (c *Container) inc(name string) {
    c.mu.Lock()
    defer c.mu.Unlock()
    c.counters[name]++
}

func main() {
    c := Container{
        counters: map[string]int{"a": 0, "b": 0},
    }

    var wg sync.WaitGroup

    doIncrement := func(name string, n int) {
        for i := 0; i < n; i++ {
            c.inc(name)
        }
        wg.Done()
    }

    wg.Add(3)
    go doIncrement("a", 10000)
    go doIncrement("a", 10000)
    go doIncrement("b", 10000)

    wg.Wait()
    fmt.Println(c.counters)
}
```

**Key Points:**
- Mutexes protect shared resources
- `Lock()` acquires the lock
- `Unlock()` releases the lock
- Always use `defer` to ensure unlock
- Prevents race conditions

---

## Stateful Goroutines

Stateful goroutines use channels to manage state instead of mutexes.

```go
package main

import (
    "fmt"
    "math/rand"
    "sync/atomic"
    "time"
)

type readOp struct {
    key  int
    resp chan int
}
type writeOp struct {
    key  int
    val  int
    resp chan bool
}

func main() {
    var readOps uint64
    var writeOps uint64

    reads := make(chan readOp)
    writes := make(chan writeOp)

    go func() {
        var state = make(map[int]int)
        for {
            select {
            case read := <-reads:
                read.resp <- state[read.key]
            case write := <-writes:
                state[write.key] = write.val
                write.resp <- true
            }
        }
    }()

    for r := 0; r < 100; r++ {
        go func() {
            for {
                read := readOp{
                    key:  rand.Intn(5),
                    resp: make(chan int)}
                reads <- read
                <-read.resp
                atomic.AddUint64(&readOps, 1)
                time.Sleep(time.Millisecond)
            }
        }()
    }

    for w := 0; w < 10; w++ {
        go func() {
            for {
                write := writeOp{
                    key:  rand.Intn(5),
                    val:  rand.Intn(100),
                    resp: make(chan bool)}
                writes <- write
                <-write.resp
                atomic.AddUint64(&writeOps, 1)
                time.Sleep(time.Millisecond)
            }
        }()
    }

    time.Sleep(time.Second)

    readOpsFinal := atomic.LoadUint64(&readOps)
    fmt.Println("readOps:", readOpsFinal)
    writeOpsFinal := atomic.LoadUint64(&writeOps)
    fmt.Println("writeOps:", writeOpsFinal)
}
```

**Key Points:**
- Single goroutine owns the state
- Other goroutines communicate via channels
- Avoids mutexes and race conditions
- More complex but sometimes clearer
- Good for complex state management

---

## Sorting

Go's `sort` package provides sorting for built-in and user-defined types.

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    strs := []string{"c", "a", "b"}
    sort.Strings(strs)
    fmt.Println("Strings:", strs)

    ints := []int{7, 2, 4}
    sort.Ints(ints)
    fmt.Println("Ints:   ", ints)

    s := sort.IntsAreSorted(ints)
    fmt.Println("Sorted: ", s)
}
```

**Key Points:**
- `sort` package provides sorting functions
- `sort.Strings()`, `sort.Ints()` for built-in types
- `sort.IntsAreSorted()` checks if sorted
- Sorts in-place

---

## Sorting by Functions

You can sort by custom functions using `sort.Slice()`.

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    people := []struct {
        Name string
        Age  int
    }{
        {"Gopher", 7},
        {"Alice", 55},
        {"Vera", 24},
        {"Bob", 75},
    }

    sort.Slice(people, func(i, j int) bool {
        return people[i].Age < people[j].Age
    })
    fmt.Println("By age:", people)

    sort.Slice(people, func(i, j int) bool {
        return people[i].Name < people[j].Name
    })
    fmt.Println("By name:", people)
}
```

**Key Points:**
- `sort.Slice()` sorts with custom comparison
- Comparison function returns `i < j`
- Can sort by any field or combination
- Flexible for complex sorting needs

---

## Panic

A `panic` typically means something went unexpectedly wrong.

```go
package main

import "os"

func main() {
    panic("a problem")

    _, err := os.Create("/tmp/file")
    if err != nil {
        panic(err)
    }
}
```

**Key Points:**
- `panic()` stops normal execution
- Panics are not exceptions
- Should be used for unrecoverable errors
- Can be recovered with `defer` and `recover`
- Panics propagate up the call stack

---

## Defer

`defer` schedules a function call to be executed after the surrounding function returns.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    f := createFile("/tmp/defer.txt")
    defer closeFile(f)
    writeFile(f)
}

func createFile(p string) *os.File {
    fmt.Println("creating")
    f, err := os.Create(p)
    if err != nil {
        panic(err)
    }
    return f
}

func writeFile(f *os.File) {
    fmt.Println("writing")
    fmt.Fprintln(f, "data")
}

func closeFile(f *os.File) {
    fmt.Println("closing")
    err := f.Close()
    if err != nil {
        fmt.Fprintf(os.Stderr, "error: %v\n", err)
        os.Exit(1)
    }
}
```

**Key Points:**
- `defer` executes function when surrounding function returns
- Deferred calls executed in LIFO order
- Common for cleanup (closing files, unlocking mutexes)
- Arguments evaluated immediately, function called later
- Useful for resource management

---

## Recover

`recover` is a built-in function that regains control of a panicking goroutine.

```go
package main

import "fmt"

func mayPanic() {
    panic("a problem")
}

func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recovered. Error:\n", r)
        }
    }()

    mayPanic()

    fmt.Println("After mayPanic()")
}
```

**Key Points:**
- `recover()` stops panic propagation
- Only works inside deferred functions
- Returns value passed to `panic()`
- Allows graceful error handling
- Use sparingly; prefer explicit error handling

---

## String Functions

The `strings` package provides many useful string functions.

```go
package main

import (
    "fmt"
    s "strings"
)

var p = fmt.Println

func main() {
    p("Contains:  ", s.Contains("test", "es"))
    p("Count:     ", s.Count("test", "t"))
    p("HasPrefix: ", s.HasPrefix("test", "te"))
    p("HasSuffix: ", s.HasSuffix("test", "st"))
    p("Index:     ", s.Index("test", "e"))
    p("Join:      ", s.Join([]string{"a", "b"}, "-"))
    p("Repeat:    ", s.Repeat("a", 5))
    p("Replace:   ", s.Replace("foo", "o", "0", -1))
    p("Replace:   ", s.Replace("foo", "o", "0", 1))
    p("Split:     ", s.Split("a-b-c-d-e", "-"))
    p("ToLower:   ", s.ToLower("TEST"))
    p("ToUpper:   ", s.ToUpper("test"))
    p()

    p("Len: ", len("hello"))
    p("Char:", "hello"[1])
}
```

**Key Points:**
- `strings` package provides string manipulation
- Many functions for searching, replacing, splitting
- Strings are immutable (operations return new strings)
- Use `strings.Builder` for efficient string building

---

## String Formatting

Go offers excellent support for string formatting with `fmt` package.

```go
package main

import (
    "fmt"
    "os"
)

type point struct {
    x, y int
}

func main() {
    p := point{1, 2}
    fmt.Printf("%v\n", p)
    fmt.Printf("%+v\n", p)
    fmt.Printf("%#v\n", p)
    fmt.Printf("%T\n", p)
    fmt.Printf("%t\n", true)
    fmt.Printf("%d\n", 123)
    fmt.Printf("%b\n", 14)
    fmt.Printf("%c\n", 33)
    fmt.Printf("%x\n", 456)
    fmt.Printf("%f\n", 78.9)
    fmt.Printf("%e\n", 123400000.0)
    fmt.Printf("%E\n", 123400000.0)
    fmt.Printf("%s\n", "\"string\"")
    fmt.Printf("%q\n", "\"string\"")
    fmt.Printf("%x\n", "hex this")
    fmt.Printf("%p\n", &p)
    fmt.Printf("|%6d|%6d|\n", 12, 345)
    fmt.Printf("|%6.2f|%6.2f|\n", 1.2, 3.45)
    fmt.Printf("|%-6.2f|%-6.2f|\n", 1.2, 3.45)
    fmt.Printf("|%6s|%6s|\n", "foo", "b")
    fmt.Printf("|%-6s|%-6s|\n", "foo", "b")

    s := fmt.Sprintf("a %s", "string")
    fmt.Println(s)

    fmt.Fprintf(os.Stderr, "an %s\n", "error")
}
```

**Key Points:**
- `fmt.Printf()` formats and prints
- `fmt.Sprintf()` returns formatted string
- `fmt.Fprintf()` writes to io.Writer
- Many format verbs: `%v`, `%d`, `%s`, `%f`, etc.
- Width and precision can be specified

---

## Text Templates

Go's `text/template` package provides templating.

```go
package main

import (
    "os"
    "text/template"
)

func main() {
    t1 := template.New("t1")
    t1, err := t1.Parse("Value is {{.}}\n")
    if err != nil {
        panic(err)
    }

    t1 = template.Must(t1.Parse("Value: {{.}}\n"))

    t1.Execute(os.Stdout, "some text")
    t1.Execute(os.Stdout, 5)
    t1.Execute(os.Stdout, []string{
        "Go",
        "Rust",
        "C++",
        "C#",
    })

    Create := func(name, t string) *template.Template {
        return template.Must(template.New(name).Parse(t))
    }

    t2 := Create("t2", "Name: {{.Name}}\n")

    t2.Execute(os.Stdout, struct {
        Name string
    }{"Jane Doe"})

    t2.Execute(os.Stdout, map[string]string{
        "Name": "Mickey Mouse",
    })

    t3 := Create("t3",
        "{{if . -}} yes {{else -}} no {{end}}\n")
    t3.Execute(os.Stdout, "not empty")
    t3.Execute(os.Stdout, "")

    t4 := Create("t4",
        "Range: {{range .}}{{.}} {{end}}\n")
    t4.Execute(os.Stdout,
        []string{
            "Go",
            "Rust",
            "C++",
            "C#",
        })
}
```

**Key Points:**
- Templates generate text from data
- `{{.}}` accesses current value
- `{{if}}`, `{{range}}` for control flow
- `template.Must()` panics on error
- Useful for code generation, HTML, config files

---

## Regular Expressions

Go's `regexp` package provides regular expression support.

```go
package main

import (
    "bytes"
    "fmt"
    "regexp"
)

func main() {
    match, _ := regexp.MatchString("p([a-z]+)ch", "peach")
    fmt.Println(match)

    r, _ := regexp.Compile("p([a-z]+)ch")

    fmt.Println(r.MatchString("peach"))

    fmt.Println(r.FindString("peach punch"))

    fmt.Println(r.FindStringIndex("peach punch"))

    fmt.Println(r.FindStringSubmatch("peach punch"))

    fmt.Println(r.FindStringSubmatchIndex("peach punch"))

    fmt.Println(r.FindAllString("peach punch pinch", -1))

    fmt.Println(r.FindAllStringSubmatchIndex(
        "peach punch pinch", -1))

    fmt.Println(r.Match([]byte("peach")))

    r = regexp.MustCompile("p([a-z]+)ch")
    fmt.Println(r)

    fmt.Println(r.ReplaceAllString("a peach", "<fruit>"))

    in := []byte("a peach")
    out := r.ReplaceAllFunc(in, bytes.ToUpper)
    fmt.Println(string(out))
}
```

**Key Points:**
- `regexp` package provides regex support
- `Compile()` or `MustCompile()` create regex
- Many methods for matching and finding
- Can work with strings or byte slices
- Supports submatch capturing

---

## JSON

Go has excellent support for JSON encoding and decoding.

```go
package main

import (
    "encoding/json"
    "fmt"
    "os"
)

type response1 struct {
    Page   int
    Fruits []string
}

type response2 struct {
    Page   int      `json:"page"`
    Fruits []string `json:"fruits"`
}

func main() {
    bolB, _ := json.Marshal(true)
    fmt.Println(string(bolB))

    intB, _ := json.Marshal(1)
    fmt.Println(string(intB))

    fltB, _ := json.Marshal(2.34)
    fmt.Println(string(fltB))

    strB, _ := json.Marshal("gopher")
    fmt.Println(string(strB))

    slcD := []string{"apple", "peach", "pear"}
    slcB, _ := json.Marshal(slcD)
    fmt.Println(string(slcB))

    mapD := map[string]int{"apple": 5, "lettuce": 7}
    mapB, _ := json.Marshal(mapD)
    fmt.Println(string(mapB))

    res1D := &response1{
        Page:   1,
        Fruits: []string{"apple", "peach", "pear"}}
    res1B, _ := json.Marshal(res1D)
    fmt.Println(string(res1B))

    res2D := &response2{
        Page:   1,
        Fruits: []string{"apple", "peach", "pear"}}
    res2B, _ := json.Marshal(res2D)
    fmt.Println(string(res2B))

    byt := []byte(`{"num":6.13,"strs":["a","b"]}`)

    var dat map[string]interface{}

    if err := json.Unmarshal(byt, &dat); err != nil {
        panic(err)
    }
    fmt.Println(dat)

    num := dat["num"].(float64)
    fmt.Println(num)

    strs := dat["strs"].([]interface{})
    str1 := strs[0].(string)
    fmt.Println(str1)

    str := `{"page": 1, "fruits": ["apple", "peach"]}`
    res := response2{}
    json.Unmarshal([]byte(str), &res)
    fmt.Println(res)
    fmt.Println(res.Fruits[0])

    enc := json.NewEncoder(os.Stdout)
    d := map[string]int{"apple": 5, "lettuce": 7}
    enc.Encode(d)
}
```

**Key Points:**
- `json.Marshal()` encodes to JSON
- `json.Unmarshal()` decodes from JSON
- Struct tags control JSON field names
- Can encode/decode maps, slices, structs
- `json.NewEncoder()` for streaming

---

## XML

Go also supports XML encoding and decoding.

```go
package main

import (
    "encoding/xml"
    "fmt"
)

type Plant struct {
    XMLName xml.Name `xml:"plant"`
    Id      int      `xml:"id,attr"`
    Name    string   `xml:"name"`
    Origin  []string `xml:"origin"`
}

func (p Plant) String() string {
    return fmt.Sprintf("Plant id=%v, name=%v, origin=%v",
        p.Id, p.Name, p.Origin)
}

func main() {
    coffee := &Plant{Id: 27, Name: "Coffee"}
    coffee.Origin = []string{"Ethiopia", "Brazil"}

    out, _ := xml.MarshalIndent(coffee, " ", "  ")
    fmt.Println(string(out))

    fmt.Println(xml.Header + string(out))

    var p Plant
    if err := xml.Unmarshal(out, &p); err != nil {
        panic(err)
    }
    fmt.Println(p)

    tomato := &Plant{Id: 81, Name: "Tomato"}
    tomato.Origin = []string{"Mexico", "California"}

    type Nesting struct {
        XMLName xml.Name `xml:"nesting"`
        Plants  []*Plant `xml:"parent>child>plant"`
    }

    nesting := &Nesting{}
    nesting.Plants = []*Plant{coffee, tomato}

    out, _ = xml.MarshalIndent(nesting, " ", "  ")
    fmt.Println(string(out))
}
```

**Key Points:**
- `xml.Marshal()` encodes to XML
- `xml.Unmarshal()` decodes from XML
- Struct tags control XML structure
- Supports attributes and nested elements
- `xml.Name` for root element name

---

## Time

Go's `time` package provides time-related functionality.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    p := fmt.Println

    now := time.Now()
    p(now)

    then := time.Date(
        2009, 11, 17, 20, 34, 58, 651387237, time.UTC)
    p(then)

    p(then.Year())
    p(then.Month())
    p(then.Day())
    p(then.Hour())
    p(then.Minute())
    p(then.Second())
    p(then.Nanosecond())
    p(then.Location())

    p(then.Weekday())

    p(then.Before(now))
    p(then.After(now))
    p(then.Equal(now))

    diff := now.Sub(then)
    p(diff)

    p(diff.Hours())
    p(diff.Minutes())
    p(diff.Seconds())
    p(diff.Nanoseconds())

    p(then.Add(diff))
    p(then.Add(-diff))
}
```

**Key Points:**
- `time.Now()` gets current time
- `time.Date()` creates specific time
- Many methods for extracting components
- Can compare times with `Before()`, `After()`, `Equal()`
- `Sub()` calculates duration

---

## Epoch

Working with Unix timestamps (epoch time).

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    now := time.Now()
    secs := now.Unix()
    nanos := now.UnixNano()
    fmt.Println(now)

    millis := nanos / 1000000
    fmt.Println(secs)
    fmt.Println(millis)
    fmt.Println(nanos)

    fmt.Println(time.Unix(secs, 0))
    fmt.Println(time.Unix(0, nanos))
}
```

**Key Points:**
- `Unix()` returns seconds since epoch
- `UnixNano()` returns nanoseconds since epoch
- `time.Unix()` creates time from timestamp
- Useful for APIs and databases

---

## Time Formatting / Parsing

Go uses a reference time for formatting: `Mon Jan 2 15:04:05 MST 2006`.

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    p := fmt.Println

    t := time.Now()
    p(t.Format(time.RFC3339))

    t1, e := time.Parse(
        time.RFC3339,
        "2012-11-01T22:08:41+00:00")
    p(t1)

    p(t.Format("3:04PM"))
    p(t.Format("Mon Jan _2 15:04:05 2006"))
    p(t.Format("2006-01-02T15:04:05.999999-07:00"))
    form := "3 04 PM"
    t2, e := time.Parse(form, "8 41 PM")
    p(t2)

    fmt.Printf("%d-%02d-%02dT%02d:%02d:%02d-00:00\n",
        t.Year(), t.Month(), t.Day(),
        t.Hour(), t.Minute(), t.Second())

    ansic := "Mon Jan _2 15:04:05 2006"
    _, e = time.Parse(ansic, "8:41PM")
    p(e)
}
```

**Key Points:**
- Reference time: `Mon Jan 2 15:04:05 MST 2006` (01/02 03:04:05PM '06 -0700)
- `Format()` converts time to string
- `Parse()` converts string to time
- Use reference time components for custom formats

---

## Random Numbers

Go's `math/rand` package provides pseudorandom number generation.

```go
package main

import (
    "fmt"
    "math/rand"
    "time"
)

func main() {
    fmt.Print(rand.Intn(100), ",")
    fmt.Print(rand.Intn(100))
    fmt.Println()

    fmt.Println(rand.Float64())

    fmt.Print((rand.Float64()*5)+5, ",")
    fmt.Print((rand.Float64() * 5) + 5)
    fmt.Println()

    s1 := rand.NewSource(time.Now().UnixNano())
    r1 := rand.New(s1)

    fmt.Print(r1.Intn(100), ",")
    fmt.Print(r1.Intn(100))
    fmt.Println()

    s2 := rand.NewSource(42)
    r2 := rand.New(s2)
    fmt.Print(r2.Intn(100), ",")
    fmt.Print(r2.Intn(100))
    fmt.Println()

    s3 := rand.NewSource(42)
    r3 := rand.New(s3)
    fmt.Print(r3.Intn(100), ",")
    fmt.Print(r3.Intn(100))
    fmt.Println()
}
```

**Key Points:**
- `math/rand` provides pseudorandom numbers
- Seed with `rand.Seed()` or `rand.NewSource()`
- Use `crypto/rand` for cryptographically secure random
- Same seed produces same sequence

---

## Number Parsing

Parsing numbers from strings.

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {
    f, _ := strconv.ParseFloat("1.234", 64)
    fmt.Println(f)

    i, _ := strconv.ParseInt("123", 0, 64)
    fmt.Println(i)

    d, _ := strconv.ParseInt("0x1c8", 0, 64)
    fmt.Println(d)

    u, _ := strconv.ParseUint("789", 0, 64)
    fmt.Println(u)

    k, _ := strconv.Atoi("135")
    fmt.Println(k)

    _, e := strconv.Atoi("wat")
    fmt.Println(e)
}
```

**Key Points:**
- `strconv` package for number parsing
- `ParseFloat()`, `ParseInt()`, `ParseUint()`
- `Atoi()` is shorthand for `ParseInt(..., 10, 0)`
- Base 0 means infer from string prefix
- Always check errors

---

## URL Parsing

Parsing URLs with Go's `net/url` package.

```go
package main

import (
    "fmt"
    "net"
    "net/url"
)

func main() {
    s := "postgres://user:pass@host.com:5432/path?k=v#f"

    u, err := url.Parse(s)
    if err != nil {
        panic(err)
    }

    fmt.Println(u.Scheme)

    fmt.Println(u.User)
    fmt.Println(u.User.Username())
    p, _ := u.User.Password()
    fmt.Println(p)

    fmt.Println(u.Host)
    host, port, _ := net.SplitHostPort(u.Host)
    fmt.Println(host)
    fmt.Println(port)

    fmt.Println(u.Path)
    fmt.Println(u.Fragment)

    fmt.Println(u.RawQuery)
    m, _ := url.ParseQuery(u.RawQuery)
    fmt.Println(m)
    fmt.Println(m["k"][0])
}
```

**Key Points:**
- `url.Parse()` parses URL strings
- Access scheme, user, host, path, query, fragment
- `ParseQuery()` parses query parameters
- `net.SplitHostPort()` splits host:port

---

## SHA256 Hashes

Go's `crypto/*` packages provide hashing functions.

```go
package main

import (
    "crypto/sha256"
    "fmt"
)

func main() {
    s := "sha256 this string"

    h := sha256.New()

    h.Write([]byte(s))

    bs := h.Sum(nil)

    fmt.Println(s)
    fmt.Printf("%x\n", bs)
}
```

**Key Points:**
- `crypto/sha256` provides SHA256 hashing
- Create hash with `New()`
- Write data with `Write()`
- Get hash with `Sum()`
- Other algorithms: `sha1`, `sha512`, `md5` (deprecated)

---

## Base64 Encoding

Go provides built-in support for base64 encoding/decoding.

```go
package main

import (
    "encoding/base64"
    "fmt"
)

func main() {
    data := "abc123!?$*&()'-=@~"

    sEnc := base64.StdEncoding.EncodeToString([]byte(data))
    fmt.Println(sEnc)

    sDec, _ := base64.StdEncoding.DecodeString(sEnc)
    fmt.Println(string(sDec))
    fmt.Println()

    uEnc := base64.URLEncoding.EncodeToString([]byte(data))
    fmt.Println(uEnc)
    uDec, _ := base64.URLEncoding.DecodeString(uEnc)
    fmt.Println(string(uDec))
}
```

**Key Points:**
- `base64` package for encoding/decoding
- `StdEncoding` for standard base64
- `URLEncoding` for URL-safe base64
- `EncodeToString()` and `DecodeString()` are convenient

---

## Reading Files

Reading files is one of the most common tasks.

```go
package main

import (
    "bufio"
    "fmt"
    "io"
    "io/ioutil"
    "os"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

func main() {
    dat, err := ioutil.ReadFile("/tmp/dat")
    check(err)
    fmt.Print(string(dat))

    f, err := os.Open("/tmp/dat")
    check(err)

    b1 := make([]byte, 5)
    n1, err := f.Read(b1)
    check(err)
    fmt.Printf("%d bytes: %s\n", n1, string(b1[:n1]))

    o2, err := f.Seek(6, 0)
    check(err)
    b2 := make([]byte, 2)
    n2, err := f.Read(b2)
    check(err)
    fmt.Printf("%d bytes @ %d: %s\n", n2, o2, string(b2[:n2]))

    o3, err := f.Seek(6, 0)
    check(err)
    b3 := make([]byte, 2)
    n3, err := io.ReadAtLeast(f, b3, 2)
    check(err)
    fmt.Printf("%d bytes @ %d: %s\n", n3, o3, string(b3))

    _, err = f.Seek(0, 0)
    check(err)

    r4 := bufio.NewReader(f)
    b4, err := r4.Peek(5)
    check(err)
    fmt.Printf("5 bytes: %s\n", string(b4))

    f.Close()
}
```

**Key Points:**
- `ioutil.ReadFile()` reads entire file
- `os.Open()` opens file for reading
- `bufio` provides buffered I/O
- `Seek()` moves file pointer
- Always close files

---

## Writing Files

Writing files in Go follows similar patterns to reading.

```go
package main

import (
    "bufio"
    "fmt"
    "io/ioutil"
    "os"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

func main() {
    d1 := []byte("hello\ngo\n")
    err := ioutil.WriteFile("/tmp/dat1", d1, 0644)
    check(err)

    f, err := os.Create("/tmp/dat2")
    check(err)

    defer f.Close()

    d2 := []byte{115, 111, 109, 101, 10}
    n2, err := f.Write(d2)
    check(err)
    fmt.Printf("wrote %d bytes\n", n2)

    n3, err := f.WriteString("writes\n")
    fmt.Printf("wrote %d bytes\n", n3)

    f.Sync()

    w := bufio.NewWriter(f)
    n4, err := w.WriteString("buffered\n")
    fmt.Printf("wrote %d bytes\n", n4)

    w.Flush()
}
```

**Key Points:**
- `ioutil.WriteFile()` writes entire file
- `os.Create()` creates file for writing
- `Write()` and `WriteString()` for writing
- `bufio.Writer` for buffered writing
- `Sync()` flushes to disk

---

## Line Filters

A line filter is a common type of program that reads from stdin, processes it, and writes to stdout.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "strings"
)

func main() {
    scanner := bufio.NewScanner(os.Stdin)

    for scanner.Scan() {
        ucl := strings.ToUpper(scanner.Text())
        fmt.Println(ucl)
    }

    if err := scanner.Err(); err != nil {
        fmt.Fprintln(os.Stderr, "error:", err)
        os.Exit(1)
    }
}
```

**Key Points:**
- `bufio.Scanner` reads line by line
- `Scan()` reads next line
- `Text()` gets current line
- Check `Err()` for errors
- Useful for command-line tools

---

## File Paths

The `filepath` package provides functions for manipulating file paths.

```go
package main

import (
    "fmt"
    "path/filepath"
    "strings"
)

func main() {
    p := filepath.Join("dir1", "dir2", "filename")
    fmt.Println("p:", p)

    fmt.Println(filepath.Join("dir1//", "filename"))
    fmt.Println(filepath.Join("dir1/../dir1", "filename"))

    fmt.Println("Dir(p):", filepath.Dir(p))
    fmt.Println("Base(p):", filepath.Base(p))
    fmt.Println("IsAbs:", filepath.IsAbs("dir/file"))
    fmt.Println("IsAbs:", filepath.IsAbs("/dir/file"))

    filename := "config.json"
    ext := filepath.Ext(filename)
    fmt.Println(ext)

    fmt.Println(strings.TrimSuffix(filename, ext))

    rel, err := filepath.Rel("a/b", "a/b/t/file")
    if err != nil {
        panic(err)
    }
    fmt.Println(rel)

    rel, err = filepath.Rel("a/b", "a/c/t/file")
    if err != nil {
        panic(err)
    }
    fmt.Println(rel)
}
```

**Key Points:**
- `filepath.Join()` builds paths correctly
- `Dir()`, `Base()`, `Ext()` extract path components
- `IsAbs()` checks if absolute path
- `Rel()` computes relative path
- Cross-platform path handling

---

## Directories

Working with directories in Go.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "os"
    "path/filepath"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

func main() {
    err := os.Mkdir("subdir", 0755)
    check(err)

    defer os.RemoveAll("subdir")

    createEmptyFile := func(name string) {
        d := []byte("")
        check(ioutil.WriteFile(name, d, 0644))
    }

    createEmptyFile("subdir/file1")

    err = os.MkdirAll("subdir/parent/child", 0755)
    check(err)

    createEmptyFile("subdir/parent/file2")
    createEmptyFile("subdir/parent/file3")
    createEmptyFile("subdir/parent/child/file4")

    c, err := ioutil.ReadDir("subdir/parent")
    check(err)

    fmt.Println("Listing subdir/parent")
    for _, entry := range c {
        fmt.Println(" ", entry.Name(), entry.IsDir())
    }

    err = os.Chdir("subdir/parent/child")
    check(err)

    c, err = ioutil.ReadDir(".")
    check(err)

    fmt.Println("Listing subdir/parent/child")
    for _, entry := range c {
        fmt.Println(" ", entry.Name(), entry.IsDir())
    }

    err = os.Chdir("../../..")
    check(err)

    fmt.Println("Visiting subdir")
    err = filepath.Walk("subdir", visit)
}

func visit(p string, info os.FileInfo, err error) error {
    if err != nil {
        return err
    }
    fmt.Println(" ", p, info.IsDir())
    return nil
}
```

**Key Points:**
- `os.Mkdir()` creates single directory
- `os.MkdirAll()` creates directory tree
- `ioutil.ReadDir()` lists directory contents
- `filepath.Walk()` recursively walks directory tree
- `os.Chdir()` changes current directory

---

## Temporary Files and Directories

Creating temporary files and directories.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "os"
    "path/filepath"
)

func check(e error) {
    if e != nil {
        panic(e)
    }
}

func main() {
    f, err := ioutil.TempFile("", "sample")
    check(err)

    fmt.Println("Temp file name:", f.Name())

    defer os.Remove(f.Name())

    _, err = f.Write([]byte{1, 2, 3, 4})
    check(err)

    dname, err := ioutil.TempDir("", "sampledir")
    fmt.Println("Temp dir name:", dname)

    defer os.RemoveAll(dname)

    fname := filepath.Join(dname, "file1")
    err = ioutil.WriteFile(fname, []byte{1, 2}, 0666)
    check(err)
}
```

**Key Points:**
- `ioutil.TempFile()` creates temporary file
- `ioutil.TempDir()` creates temporary directory
- Files/dirs created in system temp directory
- Should clean up with `Remove()` or `RemoveAll()`
- Useful for testing and temporary data

---

## Embed Directive

Go 1.16 introduced the `//go:embed` directive to embed files at compile time.

```go
package main

import (
    _ "embed"
    "fmt"
)

//go:embed hello.txt
var s string

func main() {
    fmt.Print(s)
}
```

**Key Points:**
- `//go:embed` embeds files at compile time
- Must import `_ "embed"` package
- Can embed files, directories, or patterns
- Files become part of binary
- Useful for templates, static assets

---

## Testing and Benchmarking

Go has a built-in testing package.

```go
package main

import (
    "fmt"
    "testing"
)

func IntMin(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func TestIntMinBasic(t *testing.T) {
    ans := IntMin(2, -2)
    if ans != -2 {
        t.Errorf("IntMin(2, -2) = %d; want -2", ans)
    }
}

func TestIntMinTableDriven(t *testing.T) {
    var tests = []struct {
        a, b int
        want int
    }{
        {0, 1, 0},
        {1, 0, 0},
        {2, -2, -2},
        {0, -1, -1},
        {-1, 0, -1},
    }

    for _, tt := range tests {
        testname := fmt.Sprintf("%d,%d", tt.a, tt.b)
        t.Run(testname, func(t *testing.T) {
            ans := IntMin(tt.a, tt.b)
            if ans != tt.want {
                t.Errorf("got %d, want %d", ans, tt.want)
            }
        })
    }
}

func BenchmarkIntMin(b *testing.B) {
    for i := 0; i < b.N; i++ {
        IntMin(1, 2)
    }
}
```

**Key Points:**
- Test functions start with `Test`
- Benchmark functions start with `Benchmark`
- Run tests with `go test`
- Run benchmarks with `go test -bench=.`
- Table-driven tests are common pattern

---

## Command-Line Arguments

Command-line arguments are available via `os.Args`.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    argsWithProg := os.Args
    argsWithoutProg := os.Args[1:]

    arg := os.Args[3]

    fmt.Println(argsWithProg)
    fmt.Println(argsWithoutProg)
    fmt.Println(arg)
}
```

**Key Points:**
- `os.Args` is slice of strings
- `os.Args[0]` is program name
- `os.Args[1:]` are arguments
- For complex parsing, use `flag` package

---

## Command-Line Flags

The `flag` package provides command-line flag parsing.

```go
package main

import (
    "flag"
    "fmt"
)

func main() {
    wordPtr := flag.String("word", "foo", "a string")
    numbPtr := flag.Int("numb", 42, "an int")
    boolPtr := flag.Bool("fork", false, "a bool")

    var svar string
    flag.StringVar(&svar, "svar", "bar", "a string var")

    flag.Parse()

    fmt.Println("word:", *wordPtr)
    fmt.Println("numb:", *numbPtr)
    fmt.Println("fork:", *boolPtr)
    fmt.Println("svar:", svar)
    fmt.Println("tail:", flag.Args())
}
```

**Key Points:**
- `flag.String()`, `flag.Int()`, `flag.Bool()` create flags
- `flag.StringVar()` binds to existing variable
- `flag.Parse()` parses command line
- `flag.Args()` gets non-flag arguments
- Automatic help with `-h` or `--help`

---

## Command-Line Subcommands

Go supports subcommands using the `flag` package.

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func main() {
    fooCmd := flag.NewFlagSet("foo", flag.ExitOnError)
    fooEnable := fooCmd.Bool("enable", false, "enable")
    fooName := fooCmd.String("name", "", "name")

    barCmd := flag.NewFlagSet("bar", flag.ExitOnError)
    barLevel := barCmd.Int("level", 0, "level")

    if len(os.Args) < 2 {
        fmt.Println("expected 'foo' or 'bar' subcommands")
        os.Exit(1)
    }

    switch os.Args[1] {
    case "foo":
        fooCmd.Parse(os.Args[2:])
        fmt.Println("subcommand 'foo'")
        fmt.Println("  enable:", *fooEnable)
        fmt.Println("  name:", *fooName)
        fmt.Println("  tail:", fooCmd.Args())
    case "bar":
        barCmd.Parse(os.Args[2:])
        fmt.Println("subcommand 'bar'")
        fmt.Println("  level:", *barLevel)
        fmt.Println("  tail:", barCmd.Args())
    default:
        fmt.Println("expected 'foo' or 'bar' subcommands")
        os.Exit(1)
    }
}
```

**Key Points:**
- `flag.NewFlagSet()` creates subcommand
- Each subcommand has its own flags
- Parse based on first argument
- Useful for complex CLI tools

---

## Environment Variables

Environment variables are accessed via `os.Getenv()` and `os.Setenv()`.

```go
package main

import (
    "fmt"
    "os"
    "strings"
)

func main() {
    os.Setenv("FOO", "1")
    fmt.Println("FOO:", os.Getenv("FOO"))
    fmt.Println("BAR:", os.Getenv("BAR"))

    fmt.Println()
    for _, e := range os.Environ() {
        pair := strings.SplitN(e, "=", 2)
        fmt.Println(pair[0])
    }
}
```

**Key Points:**
- `os.Getenv()` gets environment variable
- `os.Setenv()` sets environment variable
- `os.Environ()` gets all environment variables
- Returns empty string if variable not set
- Use for configuration

---

## Logging

Go's `log` package provides simple logging.

```go
package main

import (
    "bytes"
    "fmt"
    "log"
)

func main() {
    log.Printf("log.Printf")

    var buf bytes.Buffer
    logger := log.New(&buf, "logger: ", log.Lshortfile)
    logger.Print("Hello, log file!")

    fmt.Print(&buf)

    logger.SetPrefix("new logger: ")
    logger.Print("Hello again!")
    fmt.Print(&buf)
}
```

**Key Points:**
- `log` package provides basic logging
- `log.Printf()` for formatted logging
- `log.New()` creates custom logger
- Can set prefix and flags
- For advanced logging, use third-party packages

---

## HTTP Client

Go's `net/http` package provides HTTP client functionality.

```go
package main

import (
    "bufio"
    "fmt"
    "net/http"
)

func main() {
    resp, err := http.Get("https://gobyexample.com")
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    fmt.Println("Response status:", resp.Status)

    scanner := bufio.NewScanner(resp.Body)
    for i := 0; scanner.Scan() && i < 5; i++ {
        fmt.Println(scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        panic(err)
    }
}
```

**Key Points:**
- `http.Get()` makes GET request
- `http.Post()`, `http.PostForm()` for other methods
- `http.Client` for more control
- Always close response body
- Check status code

---

## HTTP Server

Creating HTTP servers with Go.

```go
package main

import (
    "fmt"
    "net/http"
)

func hello(w http.ResponseWriter, req *http.Request) {
    fmt.Fprintf(w, "hello\n")
}

func headers(w http.ResponseWriter, req *http.Request) {
    for name, headers := range req.Header {
        for _, h := range headers {
            fmt.Fprintf(w, "%v: %v\n", name, h)
        }
    }
}

func main() {
    http.HandleFunc("/hello", hello)
    http.HandleFunc("/headers", headers)

    http.ListenAndServe(":8090", nil)
}
```

**Key Points:**
- `http.HandleFunc()` registers route handler
- `http.ListenAndServe()` starts server
- Handlers have `ResponseWriter` and `Request`
- Can use `http.ServeMux` for routing
- Production servers need more features

---

## TCP Server

Creating TCP servers for low-level network programming.

```go
package main

import (
    "bufio"
    "fmt"
    "net"
    "time"
)

func main() {
    listener, err := net.Listen("tcp", ":8080")
    if err != nil {
        panic(err)
    }

    for {
        conn, err := listener.Accept()
        if err != nil {
            continue
        }

        go handleConnection(conn)
    }
}

func handleConnection(conn net.Conn) {
    defer conn.Close()

    conn.SetReadDeadline(time.Now().Add(5 * time.Second))

    scanner := bufio.NewScanner(conn)
    for scanner.Scan() {
        text := scanner.Text()
        fmt.Println("Received:", text)
        conn.Write([]byte("Echo: " + text + "\n"))
    }
}
```

**Key Points:**
- `net.Listen()` creates TCP listener
- `Accept()` accepts connections
- Handle each connection in goroutine
- `SetReadDeadline()` for timeouts
- Lower-level than HTTP

---

## Context

The `context` package provides request-scoped values, cancellation, and timeouts.

```go
package main

import (
    "context"
    "fmt"
    "time"
)

func main() {
    ctx, cancel := context.WithTimeout(context.Background(), 50*time.Millisecond)
    defer cancel()

    select {
    case <-time.After(1 * time.Second):
        fmt.Println("overslept")
    case <-ctx.Done():
        fmt.Println(ctx.Err())
    }
}
```

**Key Points:**
- `context` manages request lifecycle
- `WithTimeout()`, `WithCancel()`, `WithValue()`
- Pass context through call chain
- `Done()` channel signals cancellation
- Essential for concurrent programs

---

## Spawning Processes

Go can spawn and manage external processes.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "os/exec"
)

func main() {
    dateCmd := exec.Command("date")
    dateOut, err := dateCmd.Output()
    if err != nil {
        panic(err)
    }
    fmt.Println("> date")
    fmt.Println(string(dateOut))

    grepCmd := exec.Command("grep", "hello")
    grepIn, _ := grepCmd.StdinPipe()
    grepOut, _ := grepCmd.StdoutPipe()
    grepCmd.Start()
    grepIn.Write([]byte("hello grep\ngoodbye grep"))
    grepIn.Close()
    grepBytes, _ := ioutil.ReadAll(grepOut)
    grepCmd.Wait()
    fmt.Println("> grep hello")
    fmt.Println(string(grepBytes))

    lsCmd := exec.Command("bash", "-c", "ls -a -l -h")
    lsOut, err := lsCmd.Output()
    if err != nil {
        panic(err)
    }
    fmt.Println("> ls -a -l -h")
    fmt.Println(string(lsOut))
}
```

**Key Points:**
- `exec.Command()` creates command
- `Output()` runs and captures output
- `Start()`, `Wait()` for async execution
- Can pipe stdin/stdout/stderr
- Useful for system integration

---

## Exec'ing Processes

Go doesn't provide a classic `fork` function, but you can exec processes.

```go
package main

import (
    "os"
    "os/exec"
    "syscall"
)

func main() {
    binary, lookErr := exec.LookPath("ls")
    if lookErr != nil {
        panic(lookErr)
    }

    args := []string{"ls", "-a", "-l", "-h"}

    env := os.Environ()

    execErr := syscall.Exec(binary, args, env)
    if execErr != nil {
        panic(execErr)
    }
}
```

**Key Points:**
- `syscall.Exec()` replaces current process
- Process is replaced, not forked
- Useful for process replacement
- Unix-specific (not Windows)

---

## Signals

Handling Unix signals in Go.

```go
package main

import (
    "fmt"
    "os"
    "os/signal"
    "syscall"
)

func main() {
    sigs := make(chan os.Signal, 1)
    signal.Notify(sigs, syscall.SIGINT, syscall.SIGTERM)

    done := make(chan bool, 1)

    go func() {
        sig := <-sigs
        fmt.Println()
        fmt.Println(sig)
        done <- true
    }()

    fmt.Println("awaiting signal")
    <-done
    fmt.Println("exiting")
}
```

**Key Points:**
- `signal.Notify()` registers signal handler
- Common signals: `SIGINT`, `SIGTERM`
- Signals sent via channel
- Useful for graceful shutdown
- Unix-specific

---

## Exit

Use `os.Exit` to immediately exit with a given status.

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    defer fmt.Println("!")

    os.Exit(3)
}
```

**Key Points:**
- `os.Exit()` exits immediately
- Exit code 0 means success
- Non-zero exit codes indicate error
- Deferred functions don't run
- Use for error handling

---

## Additional Resources

- [Go Official Documentation](https://go.dev/doc/)
- [Go by Example](https://gobyexample.com/)
- [Effective Go](https://go.dev/doc/effective_go)
- [Go Tour](https://go.dev/tour/)

---

*This document covers all major Go concepts from Go by Example with additional explanations and examples.*
