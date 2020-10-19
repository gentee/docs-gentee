# System

General system functions are described here.

* [GetEnv\( str name \) str](system.md#getenv-str-name-str)
* [SetEnv\( str name, bool|int|str val \)](system.md#setenv-bool-or-int-or-str-name)
* [UnsetEnv\( str name \)](system.md#unsetenv-str-name)

## Functions

### GetEnv\(str name\) str

The _GetEnv_ function returns the value of the environment variable.

``` go
Print( GetEnv("PATH"))
// the same as
Print( $PATH )
```

### SetEnv\(bool|int|str name\)

The _SetEnv_ function assigns the specified value to the environment variable.

``` go
SetEnv("MYVARB", true)
SetEnv("MYVARI", 101)
SetEnv("MYVAR", "Test value")
// the same as
$MYVARB = true
$MYVARI = 101
$MYVARI = "Test value"
```

### UnsetEnv\(str name\)

The _UnsetEnv_ function removes the environment variable.
