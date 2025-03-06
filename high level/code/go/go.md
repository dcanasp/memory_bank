#go
Created by Google, Go (also called Golang) is a statically typed, [[compiled languages|compiled language]]. It's designed for efficiency and ease of use, combining the performance of lower-level languages like C with the simplicity of higher-level languages.

Ideal for building scalable and high-performance applications. Commonly used for cloud and **server-side applications**, **microservices**, and concurrent processing.

Go does NOT have a build in package manager. Most packages you need are on the standard library
# Theory
## Design philosophies
- Minimum amount of code
- Reduce boilerplate
- Reduce abstractions
- Not the fastest but very performant (dev speed)
- Error handling 
- Power and Expressiveness
## Data types
the most important part to understand is that go has **4** key data types. 
- Basic types: *int*, *float*, *bool*, *rune*, *byte*, *complex* 
	- These are allocated by default on the **stack**
	- when passed to a function, they get passed **by value** (a copy is made) (value semantic)
	- the numeric have their signed, unsigned, 32 64 and 128 bits counterparts
	- here also lie constants, that will always stay on the **stack**
- Composite types: *struct*, *array*
	- These are allocated by default on the **stack
	- when passed to a function, they get passed **by value** (a copy is made) (value semantic)
- Reference types: *slice*, *map*, *interface*, *channel*, *function*
	- These are allocated by default on the **heap** 
	- These types are managed **via pointers** internally.
	- when passed to a function, a copy of the pointer is made, meaning the function can modify the underlying data. (pointer semantic)
- Pointer type: *\** 
	- Pointers themselves can be allocated on the stack, but they point to variables which can be on the stack or heap.

Remember [[advance go#stack vs heap|Stack vs Heap]] is an important decision, and what you do should understand these data types to create correct code
## Constants
Constants in Go are **immutable** values **known** at **compile time**.  And are the only datatype that support type promotion.
- `const i = 1` 
- `const j int = 2`
Both of those variables are *INT* but if you perform a `1.5/i` it will be promoted to a float and operated as a float. if you used a var, it will fail. and return a `(untyped float constant) truncated to int` 

An important aspect is that in this case `1.5/i`, both are constants one is undeclared and the other is declared. But both are treated as constants

Also, Constants have a precision of *128* Bits. And can be declared multiple at a time like this: 
```go
const (
        k =1
        l = 1
    )
```
### IOTA
When working with constants they might have a pattern to them. IOTA is used to increment by *1* the previous value and used it on the next constant. Here are some examples for days where each date has a number (1 to 6):
```go
	const (
		lunes = iota
		martes
		miercoles
		// continue the rest
	)
```
another example is byteSize assignation. it will follow that complex equation to assign values (and skip where TB should be)
```go
const (
		KB float64 = 1 << (10 * (iota + 1))
		MB
		GB
		_ //skips terabytes as it's anonimous
		PB
	) 
```
## Slices
a slice is an array, but it can grow dynamically. And most importantly. You can slice it. They are created with the *make* keyword, like this: `make([]int, 2)`

Imagine a [[protocols#TCP (Transmission Control Protocol)|TCP]] package being received. if you store it in a slice, you could say `name := data[0,8]`, here you store the first 8 values, with that you can process only that and pass it to multiple functions without the overhead of the whole data slice.

Here is the key part. Any element sliced from a large slice will share the same memory spaces, and deep down you are using pointer semantics. If you modify the sliced slice it will change it's parent.

You can set an slice capacity. It will be the actual allocated length. If left blank it will be the same as the creation length. If your slice length goes over it it will  have to make a copy of the data and move it to a larger space
## Iteration
go encases all iteration in the `for` command (so there is no ~~`while`~~). the for has the regular format:
`for i:=0;i<x;i++{}` a while loop would be: `for x!=clause` or `for ;x!=clause;`. Finally there are two types of *for each*

- `for pos := range(x)` this is the same as this `for pos:=0;pos<len(x);pos++`
- `for pos,data := range(x)` this actually uses the **same** **variable** on each iteration, therefore `&data` will always be the same
```go
var data int 
for pos:=0;pos< len(x);pos++{
	data = x[pos]
}
```

> [!danger] CRITICAL 
> This is outdated. from go 1.22 both of the *for each* will do the same, they will no longer create a variable, but use pointer semantics to create a new reference to the data

In the new schema this is what this code `for pos,data := range(x)` does. therefore `&data` will always change
```go
for pos:=0;pos< len(x);pos++{
	data := x[pos]
}
```

## interfaces vs structs
An interface is a valueless type, meanwhile a struct does have a value, it has a size defined, it has meaning. Interfaces don't
## Init()
Whenever you want some functions to run before the main func. The image shows a very descriptive execution order (from farthest to close)
![[initOrderGolang.png]]
## Go routines

this file is long enough, check [[advance go]]
# Practice
## basics
- **Starting a Project:**
    
    - To initialize a new Go module, use `go mod init [module-name]`.
    - This creates a `go.mod` file which tracks your project's dependencies.
- **Basic Program Structure:**
    
    - Create a `.go` file with a `main` package and a `main` function. (it has to be main package to compile it)
    - Example:
	```go
	package main
	import "fmt"
	func main() {
	  message := greetMe("world")
	  fmt.Println(message)
	} 
	func greetMe(name string) string {
	  return "Hello, " + name + "!"
	}
	```

- Run `go build` to compile your program. (pro tip create a [[makefile]])
- **Exporting Identifiers:**  
    - In Go, an identifier (like a variable or function name) is exported if it starts with a capital letter. For example, `math.Pi` is exported, while `math.pi` is not.
- **Defer Statement:**
    - The `defer` keyword postpones the execution of a function until the surrounding function returns. It's often used for cleanup tasks.


## Importing files and packages
### My own code
- **Within the Same Package:**
    - Functions from one file can directly call functions in another file within the same package.
- **Across Different Packages:**
    - Use the package's import path to access exported identifiers.
    - Example: `import "myproject/mypackage"`
- **Exported vs. Unexported Identifiers:**
    - `func Test()` (**capital T**) is exported and accessible outside its package. `func test()` (lowercase t) is not.
### someone else code
There are two types of packages, from the **standard library** and from a third party. The standard library is really good on go, and will have **almost all** of what you could want. Mean while you need to install a dependency that is not included.
To import you do: 
```go
import (
"fmt"
)
```
that will add a standard library with it's default name

```go
import (
Printer "fmt"
)
```
now i give a **custom identifier**, so i call Printer instead of fmt

```go
import (
	"github.com/gorilla/mux"
)
```
now i imported a package that i have to download


```go
import (
_ "github.com/lib/pq""
)
```
now i created a **blank identifier**. This means the package is imported for its side effects only, and its exported names are not directly accessible

## installing dependencies
- Use `go get [package-name]` to add a new dependency.
- Example:
    `go get -u github.com/gorilla/mux`
- Run `go mod tidy` to clean up the `go.mod` and `go.sum` files.
- If you want to uninstall you do a `go get -u github.com/gorilla/mux@none`
## main packages
i will add a comment on what each package does
```go
import (
 "fmt" //for printing
 "log" //for logging
 "os" //for any low level, including opening files and env
 "database/sql" //go own orm
 "net/http" //web services
 "strconv" //parse, format, convert
 "strings" //any logic with strings, suffix, contains...
 "encoding/json" //want to use json?
 "encoding/base64" //base64?
 "crypto/tls" //load any private key to server
 "bytes" //convert to buffers
 "reflect" // some metadata that the code stores (like to see datatypes)
 "sync" //any mutex, parallelism
_ "github.com/lib/pq" //your database driver
)
```

## workspaces and modules

- **Modules:**
    - A module is a collection of Go packages. `go.mod` defines the module's dependencies.
- **Workspaces:**
    - For larger projects with multiple modules, `go.work` can be used to define a workspace. It helps in managing several modules.
## cli options

- **Build to Specific Directory:**
    - `go build -o bin/`: Compiles the program and places the binary in the specified directory.
- **Common Commands:**
    - `go run [file.go]`: Compiles and runs the Go program.
    - `go test`: Runs tests in the current module.
    - `go clean`: Removes object files and cached files.

## secret managment

- ### Using External Libraries for `.env` Files
- **`godotenv` Library:**  
    - A popular choice for handling `.env` files in Go is the `godotenv` library.
    - Install with `go get github.com/joho/godotenv`.
    - Use it to load `.env` files and access variables with `os.Getenv`.
- example:
```go
import (
    "github.com/joho/godotenv"
    "log"
    "os"
)
func main() {
    err := godotenv.Load()  // Load .env file
    if err != nil {
        log.Fatal("Error loading .env file")
    }
    secret := os.Getenv("MY_SECRET")  // Access variable
}
```

### Using Standard Library
- For production or if preferring not to use external packages, use environment variables directly.
- Set them in your [[OS]], through your deployment tool, or in your development environment.
- Access them in Go using `os.Getenv`
- example:
```go
import (
    "os"
    "log"
)
func main() {
    os.Setenv("MY_SECRET", "name")
    secret := os.Getenv("MY_SECRET")
    if secret == "" {
        log.Fatal("Environment variable not set")
    }
}

```

## error handling
### on functions
To handle errors go takes a special approach, instead of the sea of try-catch that you find on any other language. Go functions **SHOULD** return the expected value and an error. For example, the function that opens files ```
```go
func Open(name string) (file *File, err error)
```
 return the file or the error, that way you ALWAYS check if err != nil
 ```go
f, err := os.Open("filename.txt")
if err != nil {
    log.Fatal(err)
}
```
### defer/panic/recover

**defer** is to send any code to a queue, and it will be executed until the current scope finished (for example you `f := os.Open("file.txt")` and in the next line you `defer f.close()` that way when the whole execution ends, your file will close )

**panic** is the last line of defense, if for example your code needs a file to work, but you can not open it you `panic(v)`. This will stop your code and will shut down the program (only use it when really needed)

The panic will stop all normal functions and **forget** all values in the **current scope**, BUT will read any **defer**ed values or functions (so files won't corrupt when you panic). Panic needs a parameter, any value will do, this will be the value that **recover** will take

**recover** is a way to regain control after the panic, but after it left current scope. Recover **must** be on a **defer**ed function (or the panic wont let you reach it). As i said before, panic needs a value, and recover **will take** that **value**. That way it can be handled with a nil

Check this code to understand it
```go
func main(id int) int {
	var test bool = true
	willBreak() //function that will do something that may fail
	fmt.Println("am i here?", test)
	return id - 1
}
func willBreak() {
	defer func() {
		if r := recover(); r != nil {
			fmt.Println(r)
			//what you want to recover with
		}
	}()
	//do something that may fail
	panic("failure!!")
}

```
The output of this function is
```shell
failure!!
am i here? true
```
## Methods (classes)
### what are they
Go does **NOT** have **classes**. Instead of it has Methods on types. Methods are functions with a special ***receiver*** argument. And appears between the keyword `func` and the function name, like:
```go
type User struct {
	Id                  int
	...
}
func (aName *User) ReturnAll(rows *sql.Rows) {}
```
in this case, `aName` is a ***receiver*** of type pointer of Users. And to call it from another file you can
```go
var user dto.User
ids, err := user.ReturnAll(rows)
```

Think of the ***receiver*** as a `this` or `self` keywork, it manages who am i. receivers can be a **Value receiver*** or a **Pointer receiver***, depending on if it's a copy or the actual object.
### why to use them

What is the power of this? an instanceless class. Your create your object of the type you want, and create **methods** for it. Methods that would go in hand with it. For example:

```go
type MyNumber int
func (f MyNumber) Abs() int {
	if f < 0 {
		return -f
	}
	return f
}
``` 
I have created a a special `MyNumber` and can call for it's absolute value like:
```go
var f MyNumber = {some Input} 
fmt.Println(f.Abs())
```
This way i manage the state that [[oop]] does without creating a class. Also i can create the getter and setters that you would normally do.

What if i want to change it so always return the absolute value?

```go
type MyNumber int
func (f *MyNumber) Abs(){
	if f < 0 {
		f = -f
	}
}
```
As it was a ***pointer receiver*** i can change it's values (like in a class)

a good example is this:
```go
type User struct {
    Id int
	...
}
// Method with a pointer receiver
func (u *User) UpdateEmail(newEmail string) {
    u.Email = newEmail
}
// Method with a value receiver
func (v User) DisplayName() string {
    return v.Name
}
```
Then 
```go
var user User = //How ever you get this object, can be a database call
user.UpdateEmail("new@example.com")
displayName := user.DisplayName()
```
### interfaces
You can also create interfaces. An _interface type_ is defined as a set of method signatures. Take into account that. A type implements an interface by implementing its methods. There is **no explicit declaration** of intent, no "implements" keyword.

## pointers

In short. `&test` is a **pointer**, it points to the location of test, meanwhile `*test` is the **value of a pointer** OR the reference for a **pointer in a function**. So for example

```go
func ReturnAll(rows *sql.Rows) {}
```
This function expects the memory direction of a `sql.Rows` object. Meanwhile `result = append(result, *rows)` is the actual value of the rows variable.

The most important thing is that when printed, pointer objects look ugly. But the can have order. For example
i have this pointer of type User `p *User` if i try to print it i get `{33 prueba4 fake4@ { true} { true}}` But if the type has public elements i can do `p.Id` and it will give me only `33`. There is **order** **inside** of the **element**
## structures
They are very simple but essential for [[Go#Methods (classes)|methods]]
```go
type DynamoEntry struct {
	FilePath string `json:"newName"`
	BrokerEntry
	Date int64
}
```
in this example i have a struct with the 3 different element types, one as a string that has an *annotation* for any json parser, if it is parsed on json the element will be called *newName*, another one is another struct, and does NOT have a name, so all of its data will be on the same level as the other params. And finally normal int element 
## database conection
You can use an [[orm]] if you really want but the standard library is more than enough in most cases

First of all you import the `"database/sql"` module from the standard library. Then you import your [Database Drivers](https://go.dev/wiki/SQLDrivers) for example `_ "github.com/lib/pq"`

This is the example of a database creation:
```go
var DB *sql.DB

func InitDB() error {
	connStr := os.Getenv("DatabaseURI")
	var err error
	DB, err = sql.Open("postgres", connStr)
	if err != nil {
		return err
	}

	if err = DB.Ping(); err != nil {
		return err
	}

	return nil
}
```
That's it. Now you can just query
```go
db := myDB.DB
rows, err := db.Query("SELECT * FROM users where ")
```
That simple. But you get a binary mess in rows. To do something useful you have to **create** a **type** structure and **iterate** over **rows** (i like using methods for this)  
```go
type User struct {
	Id                  int
	...
}
func (p User) ReturnIds(rows *sql.Rows) ([]int, error) {
	var result []int
	//only what is bellow is needed
	for rows.Next() {
		err := rows.Scan(&p.Id, {for each columm})
		if err != nil {
			log.Print(err)
		}
		result = append(result, p.Id)
	}

	var err error = nil
	return result, err
}

```
## common errors

### multiple go workspaces in a single codebase
Whenever you have two different go.mod files, they get lost, and don't know how to behave, for this you have to create a `go.work` like this:
```go
go 1.18

use (
    ./microservice
    ./secondServer
)
```
and after that, you **have** to run the command `go work use` that will create a `go.work.sum` file to manage

### Context Deadline Exceeded

Never understood this error, It can be more complex than this, But i've gotten it (the program works perfectly and just appear from one day to another). To fix it i restarted my IDE

