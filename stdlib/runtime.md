---
nav: toc
---

# Runtime

The functions for working with a virtual machine during script execution are described here.

* [error\( int id, str text, anytype pars... \)](runtime.md#error-int-id-str-text-anytype-pars)
* [ErrID\( error err \) int](runtime.md#errid-error-err-int)
* [ErrText\( error err \) str](runtime.md#errtext-error-err-str)
* [ErrTrace\( error err \) arr.trace](runtime.md#errtrace-error-err-arr-trace)
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

```text
    error(10, `Error message %{ 10 }`)
    error(10, `Error message %d`, 10)
```

### ErrID\(error err\) int

The _ErrID_ function returns the identifier of the _err_ error. This function can be used inside **try-catch** statement for error handling.

```text
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

### Trace\(\) arr.trace

The _Trace_ function returns a stack of called functions.

