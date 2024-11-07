# Go

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
