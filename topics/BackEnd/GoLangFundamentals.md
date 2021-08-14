# GoLang Fundamentals

## Motivation

- [Why GoLang is better than other languages](https://productcoalition.com/reasons-why-golang-is-better-than-other-programming-languages-4714082bb1b1)
- [What's so great about go?](https://stackoverflow.blog/2020/11/02/go-golang-learn-fast-programming-languages/)
  - Conceived by Google engineers who were "waiting" for code compilation to complete.
  - Incorporates ease of coding, efficent code-compilation, and efficent execution.
  - Alternative for C++, Java for distributed systems and server work.
  - Go uses goroutines to handle concurrency.
  - Simplicity is in its core principles.
  - Testing & profiling is built in.

## Best Practices

- [Some Best Practices -- Slides](https://talks.golang.org/2013/bestpractices.slide#4)
- [10 Go Best Practices](https://www.bacancytechnology.com/blog/go-best-practices)
- [Go Practices](https://www.agiratech.com/12-best-golang-agile-practices-we-must-follow)
  - Reduce nesting by handling errors first.
    - Less nesting means less cognitive load on the reader.
  - Avoid duplication / repetition
  - Prioritize essential code
  - Use comments for good documentation (godoc)
  - Prevent long files
  - Shorter code
  - Use gofmt to format code.
  - import. form to test circular dependencies.

## Pros / Cons

- [Pros and Cons of GO](https://hackernoon.com/should-i-go-the-pros-and-cons-of-using-go-programming-language-8c1daf711e46)

### Pros

- Ease of use, Simplicity
- Great standard library
- Strong security
  - Strongly typed
  - Built in garbage collector
  - Very prominent in industry -- will be around for a while.
- Smart Documenation: Program will complain for lack of documentation.

### Cons

- Lack of versitality due to simplistic nature.
- Young
- No VM -- Complex go programs can "chew" through memory quickly.
- No 'niche' - Very valuable at select companies, but kinda "useless" in the larger world.
- No 'GUI' Library.

## CLI, Configuration

- `go` cli tool -- manages everything for go projects
- Two ways of organizing a go project: standard, and go modules.
- **Standard**

  - go env `GOPATH` is configured by default, depending on OS (macos is `/User/<name>/go`)
  - can change `GOPATH` by exporting it in `.bashrc` or other configuration script.
  - By default, `GOPATH` directory will have 3 main directories: `package`, `bin`, and `src`.
  - All projects live under `src`, with dependencies being installed in `package`, and binaries being compiled to `bin`.

- **Go Modules**

  - Initalized with `go mod init` (similar to `npm init -y`).
  - Dependencies are stored in `go.mod` and `go.sum` (analogous to `package.json` and `package-lock.json` respectively.)

- **Other Info about Go**

  - `go get <file>` versus `go install <file>` -- `go get` fetches & installs dependencies, while `go install` just installs them.
  - `go run <file>` -- Runs a go script.

## Language Features

- [Crash Course Code here](https://github.com/Nickzster/Go-Crash-Course)

### Arrays and Slices

- Syntax:

```go
// Array
var fruitArr [2] string
fruitArr[0] = "Apple"
fruitArr[1] = "Banana"
// Slice
fruitArr := []string {"Apple", "Banana"}
fruitArr = append(fruitArr, "Strawberry")
```

- Arrays are fixed-length arrays, while slices are dynamic arrays.

### Closures

-

- Syntax:

```go
func foo() func (string)string {
  str:= "foo"
  return func(str2 string)string {
    return str ": " + str2
  }
}

func main() {
  foo := foo()
  foobar := foo("bar")
  foobaz := foo("baz")
}
```

- Functions are first class citizens in go --> Closures --> Functional programming paradigms can be used (HOF, Currying, etc.)

### Conditionals

- Same as in other langues: if / else
- Syntax:

```go
if 2 == 2 {
  // do something if true
}

switch "foobar" {
  case "foo":
    // foo
  case "foobar":
    // foobar
  default:
    // default
}
```

### Functions

- Syntax:

```go
func functionName(param1 int param2 string) string {
  // do something with param1 and param2, and return a string.
}

```

- Go also supports return "parameters".

```go
func myFancyFunc(message string) (modifier string, newFancyMessage string) {
	myNewFancyMessage := message + " (Super fancy!)"
	return "Message:", myNewFancyMessage
}


func main(){
	fmt.Println(myFancyFunc("A message!"))
}
```

- Will print `Message: A message! (Super fancy!)`

### Interfaces

- VERY similar to an `interface` in typescript: parent types are declared with `interface` while concrete types are declared with `struct`.
- Syntax:

```go
type Aninmal interface {
  speak() string
}

type Dog struct {
  woof
}
type Cat struct {
  meow
}

func (d Dog) speak() string {
  return d.woof
}

func (c Cat) speak() string {
  return c.meow
}

func makeAnimalTalk(a Animal) {
  return a.speak();
}

func main(){
  dog := Dog{"Woof!"}
  cat := Dog{"Meow!"}

  fmt.Printf("A dog says:",makeAnimalTalk(dog))
  fmt.Printf("A cat says:",makeAnimalTalk(cat))
}
```

### Loops

- `for` is very similar to other languages.
- Go has a couple of variations on the for loop, however:

```go
i := 1
for i <= 10 {
	fmt.Println(i)
	i++
}
for i := 1; i <= 10; i++ {
	fmt.Println(i)
}
```

- Maps

  - Equivalent to JavaScript's `map` and python's `dictionary` types.
  - Syntax:

  ```go
  // Define a map between a person and their age
  people := make(map[string]int32)
  people["Alice"] = 30
  people["Bob"] = 33
  people["Eve"]= 26

  // Alternate syntax
  people := map[string]int{"Alice": 30, "Bob": 33, "Eve": 26}
  ```

### Packages

- use `import` to bring in packages. If multiple packages, use `()` to enclose them.
- Syntax:

```go
import (
	"fmt"
	"math"
  "packages/strutil"
)
```

### Pointers

- Go supports pointers, just like C++ and C.
-
- Syntax:

```go
x := 5 //Assign 'x' to 5.
y := &x // Assign 'y' to 'x's memory address.

fmt.Println(*y) // Read y's "value" from the address.

x = 10
fmt.Println(*y) // Since y is an alias to x, printing *y will show 10.

*y = 15
fmt.Println(x) // Since y's value was changed, x will also reflect this change and show 15.
```

### Range

- Similar JavaScript's `for in` and `for of`. Pulls the object out of an iterable when iterating.
- Syntax

```go
  // Array
  ids := []string{"foo", "bar", "baz", "foobar"}

  for i, id := range ids {
    fmt.Println(id)
  }

  // Map
  people := map[string]int{"Alice": 30, "Bob": 33, "Eve": 26}
  for k,v := range(people) {
    // Can access the key & value for each key-pair mapping without having to reference it.
    fmt.Printf(k, "'s age is", v)
  }
```

### Structs

- Work just like a struct in C++ and C.
- Groups pieces of data together.
- Can make "Objects" with them.

- Syntax:

```go
type Turtle struct {
  name string
  speed int
  voice string
}

func (t Turtle) speak() string {
  return "Blub blub!"
}

func (t Turtle) swim() void {
  fmt.Printf("The turtle swims", speed, "meters!")
}
```

### Variables

- Main types:

  - `string`
  - `bool`
  - `int | int8 | int16 | int32 | int64`
  - `uint | uint8 | uint16 | uint32 | unt64 | uintptr`
  - `byte | uint8`
  - `rune | int32`
  - `float32 | float64`
  - `complex64 | complex128`

- Declarations
  - `var name string = "Nick` --> Assign variable `name`, with type `string` and the ability to modify, to `"Nick"`.
  - `const isCool = true` --> Assign variable `isCool`, with implicit type `true` and without the ability to modify, to `true`.
  - `hobby := "coding"` --> Declare & assign the variable `hobby`, with implicit type `string` and implicity ability to modify, to `"coding"`.
