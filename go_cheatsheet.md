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
