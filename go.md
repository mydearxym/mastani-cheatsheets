
## basic types

{{ ::cards-header:: }}

### Hello world

#### hello.go

```go
package main

import "fmt"

func main() {
  message := greetMe("world")
  fmt.Println(message)
}

func greetMe(name string) (string) {
  return "Hello, " + name + "!"
}
```

```bash
$ go build
```

Or try it out in the [Go repl](https://repl.it/languages/go), or [A Tour of Go](https://tour.golang.org/welcome/1).

{{ ::card-item:: }}

### Variables

#### Variable declaration

```go
var msg string
msg = "Hello"
```

#### Shortcut of above (Infers type)

```go
msg := "Hello"
```

{{ ::card-item:: }}

### Constants

```go
const Phi = 1.618
```

Constants can be character, string, boolean, or numeric values.

See: [Constants](https://tour.golang.org/basics/15)


{{ ::card-item:: }}
### Strings

```go
str := "Hello"
```

```go
str := `Multiline
string`
```

Strings are of type `string`.

{{ ::card-item:: }}
### Numbers

#### Typical types

```go
num := 3          // int
num := 3.         // float64
num := 3 + 4i     // complex128
num := byte('a')  // byte (alias for uint8)
```

#### Other types

```go
var u uint = 7        // uint (unsigned)
var p float32 = 22.7  // 32-bit float
```
{{ ::card-item:: }}

### Arrays

```go
// var numbers [5]int
numbers := [...]int{0, 0, 0, 0, 0}
```

Arrays have a fixed size.

{{ ::card-item:: }}
### Slices

```go
slice := []int{2, 3, 4}
```

```go
slice := []byte("Hello")
```

Slices have a dynamic size, unlike arrays.

{{ ::card-item:: }}
### Pointers

```go
func main () {
  b := *getPointer()
  fmt.Println("Value is", b)
}
```

```go
func getPointer () (myPointer *int) {
  a := 234
  return &a
}
```

Pointers point to a memory location of a variable. Go is fully garbage-collected.

See: [Pointers](https://tour.golang.org/moretypes/1)

{{ ::card-item:: }}
### Type conversions

```go
i := 2
f := float64(i)
u := uint(i)
```

See: [Type conversions](https://tour.golang.org/basics/13)

{{ ::group:: }}
## Flow control
{{ ::cards-header:: }}

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

See: [If](https://tour.golang.org/flowcontrol/5)
{{ ::card-item:: }}
### Statements in if

```go
if _, err := getResult(); err != nil {
  fmt.Println("Uh oh")
}
```

A condition in an `if` statement can be preceded with a statement before a `;`.

See: [If with a short statement](https://tour.golang.org/flowcontrol/6)

{{ ::card-item:: }}
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

See: [Switch](https://github.com/golang/go/wiki/Switch)

{{ ::group:: }}
## Functions
{{ ::cards-header:: }}

### Lambdas

```go
myfunc := func() bool {
  return x > 10000
}
```

Functions are first class objects.

{{ ::card-item:: }}
### Multiple return types

```go
a, b := getMessage()
```

```go
func getMessage() (a string, b string) {
  return "Hello", "World"
}
```

{{ ::card-item:: }}
### Named return values

```go
func split(sum int) (x, y int) {
  x := sum * 4 / 9
  y := sum - x
  return
}
```

By defining the return value names in the signature, a `return` (no args) will return variables with those names.

See: [Named return values](https://tour.golang.org/basics/7)

{{ ::group:: }}
## Packages
{{ ::cards-header:: }}

### Importing

```go
import "fmt"
import "math/rand"
```

```go
import (
  "fmt"        // gives fmt.Println
  "math/rand"  // gives rand.Intn
)
```

Both are the same.

See: [Importing](https://tour.golang.org/basics/1)

{{ ::card-item:: }}
### Aliases

```go
import r "math/rand"
```

```go
r.Intn()
```

{{ ::card-item:: }}
### Exporting names

```go
func Hello () {
  路路路
}
```

Exported names begin with capital letters.

See: [Exported names](https://tour.golang.org/basics/3)

{{ ::card-item:: }}
### Packages

```go
package hello
```

Every package file has to start with `package`.

{{ ::group:: }}

## Concurrency
{{ ::cards-header:: }}

### Goroutines

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
```

```go
func push(name string, ch chan string) {
  msg := "Hey, " + name
  ch <- msg
}
```

Channels are concurrency-safe communication objects, used in goroutines.

See: [Goroutines](https://tour.golang.org/concurrency/1), [Channels](https://tour.golang.org/concurrency/2)

{{ ::card-item:: }}
### Buffered channels

```go
ch := make(chan int, 2)
ch <- 1
ch <- 2
ch <- 3
// fatal error:
// all goroutines are asleep - deadlock!
```

Buffered channels limit the amount of messages it can keep.

See: [Buffered channels](https://tour.golang.org/concurrency/3)

{{ ::card-item:: }}

### Closing channels

#### Closes a channel

```go
ch <- 1
ch <- 2
ch <- 3
close(ch)
```

#### Iterates across a channel until its closed

```go
for i := range ch {
  路路路
}
```

#### Closed if `ok == false`

```go
v, ok := <- ch
```

See: [Range and close](https://tour.golang.org/concurrency/4)

{{ ::group:: }}

## Error control

{{ ::cards-header:: }}
### Defer

```go
func main() {
  defer fmt.Println("Done")
  fmt.Println("Working...")
}
```

Defers running a function until the surrounding function returns.
The arguments are evaluated immediately, but the function call is not ran until later.

See: [Defer, panic and recover](https://blog.golang.org/defer-panic-and-recover)

{{ ::card-item:: }}
### Deferring functions

```go
func main() {
  defer func() {
    fmt.Println("Done")
  }()
  fmt.Println("Working...")
}
```

Lambdas are better suited for defer blocks.

{{ ::group:: }}
## Structs
{{ ::cards-header:: }}

### Defining

```go
type Vertex struct {
  X int
  Y int
}
```

```go
func main() {
  v := Vertex{1, 2}
  v.X = 4
  fmt.Println(v.X, v.Y)
}
```

See: [Structs](https://tour.golang.org/moretypes/2)

{{ ::card-item:: }}
### Literals

```go
v := Vertex{X: 1, Y: 2}
```

```go
// Field names can be omitted
v := Vertex{1, 2}
```

```go
// Y is implicit
v := Vertex{X: 1}
```

You can also put field names.

{{ ::card-item:: }}
### Pointers to structs

```go
v := &Vertex{1, 2}
v.X = 2
```

Doing `v.X` is the same as doing `(*v).X`, when `v` is a pointer.

{{ ::group:: }}
## Methods
{{ ::cards-header:: }}

### Receivers

```go
type Vertex struct {
  X, Y float64
}
```

```go
func (v Vertex) Abs() float64 {
  return math.Sqrt(v.X * v.X + v.Y * v.Y)
}
```

```go
v: = Vertex{1, 2}
v.Abs()
```

There are no classes, but you can define functions with _receivers_.

See: [Methods](https://tour.golang.org/methods/1)

{{ ::card-item:: }}
### Mutation

```go
func (v *Vertex) Scale(f float64) {
  v.X = v.X * f
  v.y = v.Y * f
}
```

```go
v := Vertex{6, 12}
v.Scale(0.5)
// `v` is updated
```

By defining your receiver as a pointer (`*Vertex`), you can do mutations.

See: [Pointer receivers](https://tour.golang.org/methods/4)

{{ ::card-item:: }}

### References

- [A tour of Go](https://tour.golang.org/welcome/1) _(tour.golang.org)_
- [Golang wiki](https://github.com/golang/go/wiki/) _(github.com)_
