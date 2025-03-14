<!-- Code generated by gomarkdoc. DO NOT EDIT -->

# Forked from princjef/mageutil

The main package does not log download urls so this temporary fork allows us to see what bintool download url is being used.

# shellcmd

```go
import "github.com/parkertr/mageutil/shellcmd"
```

Package shellcmd provides utilites to define and execute shell commands\.

The core construct for executing commands is the shellcmd\.Command type\, which represents a command string as it would be typed into a terminal\. Command strings follow the same quoting and escaping rules as a typical POSIX shell\, but do not perform shell expansions\.

Once a command has been created\, it can be run using the Run\(\) method\. This will print the command that is being run and will pipe its output to the terminal\.

```
err := shellcmd.Command(`go test ./...`).Run()
```

If you need to run multiple commands in sequence\, you can do so with the shellcmd\.RunAll\(\) function\. This will handle capturing errors in previous commands and skipping execution of later commands if they fail\.

```
err := shellcmd.RunAll(
	"go test -coverprofile=coverage.out ./...",
	"go tool cover -html=coverage.out",
)
```

Commands can also run in a mode that captures their output rather than piping it to the console\. This is available via the Output\(\) method\.

```
out, err := shellcmd.Command(`go test ./...`).Output()
```

## Index

- [func RunAll(commands ...Command) error](<#func-runall>)
- [type Command](<#type-command>)
  - [func (c Command) Output() ([]byte, error)](<#func-command-output>)
  - [func (c Command) Run() error](<#func-command-run>)


## func [RunAll](<https://github.com/parkertr/mageutil/blob/master/shellcmd/shellcmd.go#L61>)

```go
func RunAll(commands ...Command) error
```

RunAll executes all of the provided commands in sequence\, only executing the next command if the previous command succeeded\. If any of the commands fail\, the rest are not executed and the error is returned\.

## type [Command](<https://github.com/parkertr/mageutil/blob/master/shellcmd/shellcmd.go#L14>)

Command defines a command which can be defined and run with output piped to stdout/stderr\.

```go
type Command string
```

### func \(Command\) [Output](<https://github.com/parkertr/mageutil/blob/master/shellcmd/shellcmd.go#L32>)

```go
func (c Command) Output() ([]byte, error)
```

Output executes the command\, capturing its stdout and stderr into a \[\]byte\, which is returned when the command completes\.

### func \(Command\) [Run](<https://github.com/parkertr/mageutil/blob/master/shellcmd/shellcmd.go#L18>)

```go
func (c Command) Run() error
```

Run executes the command\, piping its output to stdout/stderr and reporting any errors surfaced by it\.



Generated by [gomarkdoc](<https://github.com/princjef/gomarkdoc>)
