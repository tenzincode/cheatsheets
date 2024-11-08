# Go

## Table of Contents

- [Variables](#variables)
- [Constants](#constants)
- [Basic Types](#basic-types)
- [Flow Control](#flow-control)
- [Functions](#functions)
- [Packages](#packages)
- [Concurrency](#concurrency)
- [Error Control](#error-control)
- [Structs](#structs)
- [Methods](#methods)
- [Interfaces](#interfaces)

## Variables

### Declaration

```go
var msg string
var msg = "Hello, world!"
var msg string = "Hello, world!"
var x, y int
var x, y int = 1, 2
var x, msg = 1, "Hello, world!"
msg = "Hello"
```

### Declaration List

```go
var (
  x int
  y = 20
  z int = 30
  d, e = 40, "Hello"
  f, g string
)
```

### Type Inference

```go
msg := "Hello"
x, msg := 1, "Hello"
```

## Constants

Constants can be character, string, boolean, or numeric values.

```go
const Phi = 1.618
const Size int64 = 1024
const x, y = 1, 2
const (
  Pi = 3.14
  E  = 2.718
)
const (
  Sunday = iota
  Monday
  Tuesday
  Wednesday
  Thursday
  Friday
  Saturday
)
```

## Basic Types

### Strings

Strings are of type `string`.

```go
str := "Hello"
str := `Multiline
string`
```

### Numbers

```go
num := 3          // int
num := 3.         // float64
num := 3 + 4i     // complex128
num := byte('a')  // byte (alias for uint8)

var u uint = 7        // uint (unsigned)
var p float32 = 22.7  // 32-bit float
```

### Arrays

Arrays have a fixed size.

```go
// var numbers [5]int
numbers := [...]int{0, 0, 0, 0, 0}
```

### Slices

Slices have a dynamic size, unlike arrays.

```go
slice := []int{2, 3, 4}
slice := []byte("Hello")
```

### Pointers

Pointers point to a memory location of a variable. Go is fully garbage-collected.

```go
func main () {
  b := *getPointer()
  fmt.Println("Value is", b)
}
func getPointer () (myPointer *int) {
  a := 234
  return &a
}
a := new(int)
*a = 234
```

### Type Conversions

```go
i := 2
f := float64(i)
u := uint(i)
```

## Flow Control

### Conditional

```go
if day == "sunday" || day == "saturday" {
  rest()
} else if day == "monday" && isTired() {
  groan()
} else {
  work()
}
```

### Statements in if

A condition in an `if` statement can be preceded with a statement before a `;`. Variables declared by the statement are only in scope until the end of the `if`.

```go
if _, err := doThing(); err != nil {
  fmt.Println("Uh oh")
}
```

### Switch

```go
switch day {
  case "sunday":
    // cases don't "fall through" by default!
    fallthrough

  case "saturday":
    rest()

  default:
    work()
}
```

### For Loop

```go
for count := 0; count <= 10; count++ {
  fmt.Println("My counter is at", count)
}
```

### For-Range Loop

```go
entry := []string{"Jack","John","Jones"}
for i, val := range entry {
  fmt.Printf("At position %d, the character %s is present\n", i, val)
}
```

### While Loop

```go
n := 0
x := 42
for n != x {
  n := guess()
}
```

## Functions

### Lambdas

Functions are first class objects.

```go
myfunc := func() bool {
  return x > 10000
}
```

### Multiple Return Types

```go
a, b := getMessage()

func getMessage() (a string, b string) {
  return "Hello", "World"
}
```

### Named Return Values

By defining the return value names in the signature, a `return` (no args) will return variables with those names.

```go
func split(sum int) (x, y int) {
  x = sum * 4 / 9
  y = sum - x
  return
}
```

## Packages

### Importing

Both of the following are the same:

```go
import "fmt"
import "math/rand"

import (
  "fmt"        // gives fmt.Println
  "math/rand"  // gives rand.Intn
)
```

### Aliases

```go
import r "math/rand"
r.Intn()
```

### Exporting

Exported names begin with capital letters.

```go
func Hello () {
  ···
}
```

### Packages

Package files begin with `package`

```go
package hello
```

## Concurrency

### Goroutines

Channels are concurrency-safe communication objects, used in goroutines.

```go
func main() {
  // A "channel"
  ch := make(chan string)

  // Start concurrent routines
  go push("Moe", ch)
  go push("Larry", ch)
  go push("Curly", ch)

  // Read 3 results
  // (Since our goroutines are concurrent,
  // the order isn't guaranteed!)
  fmt.Println(<-ch, <-ch, <-ch)
}
func push(name string, ch chan string) {
  msg := "Hey, " + name
  ch <- msg
}
```

### Buffered Channels

Buffered channels limit the amount of messages it can keep.

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
ch <- 3
// fatal error:
// all goroutines are asleep - deadlock!
```

### Closing Channels

```go
// Close a channel
ch <- 1
ch <- 2
ch <- 3
close(ch)

// Iterate across a channel until its closed
for i := range ch {
  ···
}

// Closed if `ok == false`
v, ok := <- ch
```

### WaitGroup

A WaitGroup waits for a collection of goroutines to finish.  The main goroutine calls `Add` to set the number of goroutines to wait for.  The goroutine calls `wg.Done()` when it finishes.

```go
import "sync"

func main() {
  var wg sync.WaitGroup

  for _, item := range itemList {
    // Increment WaitGroup Counter
    wg.Add(1)
    go doOperation(&wg, item)
  }
  // Wait for goroutines to finish
  wg.Wait()

}

func doOperation(wg *sync.WaitGroup, item string) {
  defer wg.Done()
  // do operation on item
  // ...
}
```

## Error Control

### Defer

Defers running a function until the surrounding function returns.  The arguments are evaluated immediately, but the function call is not run until later.

```go
func main() {
  defer fmt.Println("Done")
  fmt.Println("Working...")
}
```

### Deferring Functions

Lambdas are better suited for defer blocks.

```go
func main() {
  defer func() {
    fmt.Println("Done")
  }()
  fmt.Println("Working...")
}
```

The `defer func` uses current value of `d`, unless we use a pointer to get final value at end of main.

```go
func main() {
  var d = int64(0)
  defer func(d *int64) {
    fmt.Printf("& %v Unix Sec\n", *d)
  }(&d)
  fmt.Print("Done ")
  d = time.Now().Unix()
}
```

## Structs

### Defining

```go
type Vertex struct {
  X int
  Y int
}

func main() {
  v := Vertex{1, 2}
  v.X = 4
  fmt.Println(v.X, v.Y)
}
```

### Literals

You can also put field names.

```go
v := Vertex{X: 1, Y: 2}

// Field names can be omitted
v := Vertex{1, 2}

// Y is implicit
v := Vertex{X: 1}
```

### Pointers to Structs

Doing `v.X` is the same as doing `(*v).x`, when `v` is a pointer.

```go
v := &Vertex{1, 2}
v.X = 2
```

## Methods

### Receivers

There are no classes, but you can define functions with receivers.

```go
type Vertex struct {
  X, Y float64
}

func (v Vertex) Abs() float64 {
  return math.Sqrt(v.X * v.X + v.Y * v.Y)
}

v := Vertex{1, 2}
v.Abs()
```

### Mutation

By defining your receiver as a pointer `*Vertex`, you can do mutations.

```go
func (v *Vertex) Scale(f float64) {
  v.X = v.X * f
  v.Y = v.Y * f
}

v := Vertex{6, 12}
v.Scale(0.5)
// `v` is updated
```

## Interfaces

### Basic Interface

```go
type Shape interface {
  Area() float64
  Perimeter() float64
}
```

### Struct

Struct `Rectangle` implicitly implements interface `Shape` by implementing all of its methods.

```go
type Rectangle struct {
  Length, Width float64
}
```

### Methods

The methods defined in `Shape` are implemented in `Rectangle`

```go
func (r Rectangle) Area() float64 {
  return r.Length * r.Width
}

func (r Rectangle) Perimeter() float64 {
  return 2 * (r.Length + r.Width)
}
```

### Interface Example

```go
func main() {
  var r Shape = Rectangle{Length: 3, Width: 4}
  fmt.Printf("Type of r: %T, Area: %v, Perimeter: %v.", r, r.Area(), r.Perimeter())
}
```
