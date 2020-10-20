---
nav: toc
---

# Runtime

The functions for working with a virtual machine during script execution are described here.

* [error\( int id, str text, anytype pars... \)](runtime.md#error-int-id-str-text-anytype-pars)
* [ErrID\( error err \) int](runtime.md#errid-error-err-int)
* [ErrText\( error err \) str](runtime.md#errtext-error-err-str)
* [ErrTrace\( error err \) arr.trace](runtime.md#errtrace-error-err-arr-trace)
* [exit\( int code \)](runtime.md#exit-int-code)
* [Progress\( int id inc \)](runtime.md#progress-int-id-inc)
* [ProgressEnd\( int id \)](runtime.md#progressend-int-id)
* [ProgressStart\( int total ptype, str src dest \) int](runtime.md#progressstart-int-total-ptype-str-src-dest-int)
* [Trace\(\) arr.trace](runtime.md#trace-arr-trace)

## Types

### trace

The _trace_ type is used to store information about the called function and has the following fields:

* **str Path** - filename
* **str Entry** - current function
* **str Func** - called function
* **int Line** - the line in the source code
* **int Pos** - the position in the line where the function was called

## Functions

### error\(int id, str text, anytype pars...\)

The _error_ function throws a custom runtime error.

* _id_ - the identifier of the error,
* _text_ - the text of the error,
* _pars_ - optional parameters. If they are specified, then _text_ must contain an appropriate template

  as in [Format](https://gentee.github.io/stdlib/string#formatstr-s-anytype-args-str) function.

```go
    error(10, `Error message %{ 10 }`)
    error(10, `Error message %d`, 10)
```

### ErrID\(error err\) int

The _ErrID_ function returns the identifier of the _err_ error. This function can be used inside **try-catch** statement for error handling.

```go
run {
  try {
    .....
    error(101, `oooops`)
  }
  catch err {
    if ErrID(err) == 101 {
      recover
    } elif ErrID(err) < 100 {
      retry
    }
  }
}
```

### ErrText\(error err\) str

The _ErrText_ function returns the text of the _err_ error. This function can be used inside **try-catch** statement for error handling.

### ErrTrace\(error err\) arr.trace

The _ErrTrace_ function returns the stack of called functions at the moment when the _err_ error occurs. This function can be used inside **try-catch** statement for error handling.

### exit\(int code\)

The _exit_ function terminates the script. The function can be called in any thread. The script returns the value of _code_.

```go
func ok(int par) int {
  if par == 0 : exit(0)
  return 3 * par
}
run int {
  int sum
  for i in 10..-10 {
    sum += ok(i)
  }
  return sum
}
```

### Progress\( int id inc \)

The _Progress_ function increases the process counter by the value of parameter _inc_. _id_ is the progress bar identifier returned by the _ProgressStart_ function. The _Progress_ function calls Go function _ProgressFunc_ which must be defined in the settings when the script starts.

``` go
  int total = 200
  int prog = ProgressStart(total, 100, `counter`, ``)
  for i in 1...5 {
    Progress(prog, 40)
  }
  ProgressEnd(prog)
```

### ProgressEnd\( int id \)

The _ProgressEnd_ function removes the process counter with the _id_ identifier.

### ProgressStart\( int total ptype, str src dest \) int

The _ProgressStart_ function creates a process counter and returns its identifier. _total_ is the maximum counter value. _ptype_ - counter type, can be any number. _src_ is the name of the source. _dest_ is the name of the target. The functions for working with the progress bar do not display anything, they call the _ProgressFunc_ function, which should be defined in [settings](/golang/reference.md) when running the script. In the _ProgressFunc_ function you can display the state of the process in a way that is convenient for you. After you have finished working with this counter you must call _ProgressEnd_ to delete it.

### Trace\(\) arr.trace

The _Trace_ function returns a stack of called functions.
