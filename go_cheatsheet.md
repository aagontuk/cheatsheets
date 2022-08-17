### Hello world ###

```go
package main

import "fmt"

func main() {
  fmt.Println("hello, world")
}
```

* Every program is made up of packages
* program starts running in package main

### Functions ###

* Types come after the variable name
* Bellow function takes two integer and returns one integer

```go
func add(x int, y int) int {
  return x + y
}
```

* Type can be crammed together if same type

```go
func add(x, y int) int {
  return x + y
}
```

* Multiple values can be returned from functions

```go
func swap(x, y string) (string, string) {
  retrun y, x
}

func main() {
  a, b := swap("hello", "world")
  fmt.Println(a, b)
}
```
```
$ world hello
```

* Values can be returned by name. If a variable name is specified
with the return type. Those variable will be return by the function.

```go
func plus_five(x, y int) (a, b int) {
  a = x + 5
  b = y + 5
  return
}

func main() {
  fmt.Println(plus_five(10, 20))
}
```
```
$ 15 25
```

### Variables ###

* `var` declares a list of variables

```go
var i, j int = 10, 20

var isGo bool
isGo = true

// Can't mix types in var
//var k int, isC bool

// implicit type declaration can be mixed
var k, isC = 25, false

fmt.Println(i, j, isGo, k, isC)
```

* `:=` can be used for short

```go
k, isC = 25, false
```

### Basic Types ###

```
bool

string

int  int8  int16  int32  int64
uint uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128
```

* Uninitialized variables are given default zero values. 0 for int, "" for strings
and false for bools

* If type isn't specified explicitly type is inferenced from the context
```go
i := 10 // i is int
hello := "hello, world" // hello is string
```

* Type conversion is done with T(v)
```go
i := 10
d := float64(i)
```

* constants are declared with `const` keyword. Constants can be declared with
`:=`.
```
const PI = 3.14
```

### Conditional statements ###

#### if/else if/else ####

```go
package main

import (
  "fmt"
  "bufio"
  "strconv"
  "strings"
  "os"
)

func main() {
  reader := bufio.NewReader(os.Stdin)
  strInp, _ := reader.ReadString('\n')
  strInp = strings.TrimSpace(strInp)
  
  intInp, _ := strconv.Atoi(strInp)

  if intInp < 0 {
    fmt.Println("negative")
  } else if intInp > 0 {
    fmt.Println("positive")
  } else {
    fmt.Println("zero")
  }
}
```

* If condition with statement. Variable scope declared in the statement
is inside if
```go
package main

import (
  "fmt"
  "math"
)

func main() {
  x := -20
  if v := math.Abs(float64(x)); v >= 10 {
    fmt.Println("Too large to process: ", v)
  }
}
```

#### Switch ####

* No fall through cases

```go
package main

import (
  "fmt"
  "math/rand"
  "time"
)

func cast_spell() string {
  spells := []string{
    "Oculus Reparo",
    "Alohomora",
    "Wingardium Leviosa",
  }

  max := len(spells) - 1

  rand.Seed(time.Now().UnixNano())

  index := rand.Intn(max + 1)

  return spells[index]
}

func main() {
  switch spell := cast_spell(); spell {
  case "Oculus Reparo":
    fix_glass()
  case "Alohomora":
    unlock()
  case "Wingardium Leviosa":
    float_object()
  default:
    break_wand()
  }
}
```
