#todo 
# Go routines
they work on green threads
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
# Build tags
https://assets.digitalocean.com/books/how-to-code-in-go.pdf
`go build -tags pro`
