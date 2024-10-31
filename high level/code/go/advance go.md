#todo 
# Go routines
they work on green threads
# Build tags
https://assets.digitalocean.com/books/how-to-code-in-go.pdf
`go build -tags pro`
# stack vs heap
Stack is self cleaning, stack is faster. Heap has garbage collector
if a function returns a pointer that must be stored on the heap. or it it is declared on the global scope.

That is the scape analysis. If something inside a function is going to remain alive (like a pointer) that value escapes and the compiler will store it in the heap. If not it goes to the stack

if you want to check the scape analysis you can use build tags like this `go build -gcflags -m=2`

## scalability
if your code (at runtime) starts growing, deploying new go routines, new stack, and filling it's space. There will be a point where the stack has to be migrated to a bigger contiguous stack. If any data is shared between stacks, it will have to change on all (like a pointer to a variable in the moving stack). For this reason for data that will be **shared** by a **lot of stacks**; it's better to **allocate** it on the **heap**
# fmt
the library used for writing is actually really cost full. In terms of compiler function cost. A simple print of `fmt.Println()` has a cost of 80. this is around 20 times more than what it costs to assign a variable and perform a sum to it. This is mainly because the `fmt.Println()` function is not trivial; it involves reflection and interfaces

This is very important to know, because if the function is "cheap" enough it can be optimized with things like function inlining. But if it goes past a defined at compile time budget; It wont be optimized. In other words. Don't leave prints that you don't need

# profiler
A profiler is 
there are two main profilers
## runtime profiler

## net profiler

from this package `"net/http/pprof"`
you add this code under your router declaration `r := http.NewServeMux()`
```go
	r.HandleFunc("/debug/pprof/", pprof.Index)
	r.HandleFunc("/debug/pprof/cmdline", pprof.Cmdline)
	r.HandleFunc("/debug/pprof/profile", pprof.Profile)
	r.HandleFunc("/debug/pprof/symbol", pprof.Symbol)
	r.HandleFunc("/debug/pprof/trace", pprof.Trace)

	r.Handle("/debug/pprof/block", pprof.Handler("block"))
	r.Handle("/debug/pprof/goroutine", pprof.Handler("goroutine"))
	r.Handle("/debug/pprof/heap", pprof.Handler("heap"))
	r.Handle("/debug/pprof/threadcreate", pprof.Handler("threadcreate"))
```
and with that you are set. 

you can use go tools to see the data: for example
```
go tool pprof -seconds 60 myserver http://localhost:3004/debug/pprof/profile

go tool pprof 
http://localhost:3004/debug/pprof/heap

go tool pprof http://localhost:3004/debug/pprof/block

go tool pprof http://localhost:3004/debug/pprof/goroutine
```
inside of any of those you can do a *top* to see the usage of each of those categories, for example the cpu Usage of 60 seconds
![[goProfilerCpu.png]]

or the heap usage 
![[goProfillerHeap.png]]

# building other OS
```shell
GOOS=wasip1 GOARCH=wasm go build -o main.wasm main.go
```
`GOOS` - Target Operating System
`GOARCH` - Target Platform
# Jupyter
this is not something that go offers. but [janpfeifer](https://github.com/janpfeifer/gonb) created a [[docker]] image to use jupyter notebooks with docker