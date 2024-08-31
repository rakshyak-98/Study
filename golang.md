### setup debugger
- prerequisite
	- install Delve debugger for golang
```bash
go install github.com/go-delve/delve/cmd/dlv@latest
```

> [!NOTE] include debugging symbols in the binary. These symbols provide essential information to the debugger about the structure and flow of your code. Without these symbols, the debugger would not be able to provide meaningful insights into the state of your program during execution.

```bash
go build -gcflags="all=-N -l" -o <my-app> 
```
	
```json
{
	"configuration": [
		{
			
		}
	]
}
```

### panic build in function
- `panic` and `recover` are function-scoped, unlike `try/catch` which is block-scoped. This means you can only recover from a panic withing the same function using a deferred function.
- only for truly exceptional, unrecoverable situations, not for regular error handling. Errors are expected to be handled explicitly by returning them from functions.
- Error handling in Go is more verbose, as you need to explicitly check for errors after every operation. This verbosity is intentional to encourage better error handling practices.
- Propagation : when a `panic` occurs, it unwinds the stack, running deferred function until it reaches the top-level, unlike exception which can be caught at any level.
- `panic/recover` are generally faster than exception because they don't carry the full stack trace.