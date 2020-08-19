# Constants

## Predefined constants

### CYCLE

Maximum number of iterations in a cycle. By default, it is 1600000000.

### DEPTH

Maximum nesting of executable blocks. Limits the recursion depth. By default, it is equal to 1000.

### IOTA

The _IOTA_ constant is used to automatically calculate the sequence of constants.

````go
const IOTA * 2 {"a6}
    ZERO // 0
    TWO // 2
    FOUR // 4
}
```

### SCRIPT

The _SCRIPT_ constant returns the path of the current script. If it was not specified, the _run_ name is returned.

```go
// compile from file: /home/ak/gentee/scripts/myscript.g
run {
    Println(SCRIPT) // /home/ak/gentee/scripts/myscript.g
}

// compile from memory
run my_best_script {
    Println(SCRIPT) // my_best_script
}
```

### VERSION

The _VERSION_ constant returns the current version of the Gentee compiler.
