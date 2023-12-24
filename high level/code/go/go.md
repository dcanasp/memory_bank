## why/use cases

Created by Google, Go (also called Golang) is a statically typed, [[compiled languages||compiled language]]. It's designed for efficiency and ease of use, combining the performance of lower-level languages like C with the simplicity of higher-level languages.

Ideal for building scalable and high-performance applications. Commonly used for cloud and **server-side applications**, **microservices**, and concurrent processing.

Go does NOT have a build in package manager. Most packages you need are on the standar library
## basics
- **Starting a Project:**
    
    - To initialize a new Go module, use `go mod init [module-name]`.
    - This creates a `go.mod` file which tracks your project's dependencies.
- **Basic Program Structure:**
    
    - Create a `.go` file with a `main` package and a `main` function.
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
`
- Run `go build` to compile your program.
- **Exporting Identifiers:**  
    - In Go, an identifier (like a variable or function name) is exported if it starts with a capital letter. For example, `math.Pi` is exported, while `math.pi` is not.
- **Defer Statement:**
    
    - The `defer` keyword postpones the execution of a function until the surrounding function returns. It's often used for cleanup tasks.

## installing dependencies

- Use `go get [package-name]` to add a new dependency.
- Example:
    `go get -u github.com/gorilla/mux`
- Run `go mod tidy` to clean up the `go.mod` and `go.sum` files.

## Importing files and packages
- **Within the Same Package:**
    - Functions from one file can directly call functions in another file within the same package.
- **Across Different Packages:**
    - Use the package's import path to access exported identifiers.
    - Example: `import "myproject/mypackage"`
- **Exported vs. Unexported Identifiers:**
    - `func Test()` (capital T) is exported and accessible outside its package. `func test()` (lowercase t) is not.

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

### ### Using Standard Library
- For production or if preferring not to use external packages, use environment variables directly.
- Set them in your OS, through your deployment tool, or in your development environment.
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