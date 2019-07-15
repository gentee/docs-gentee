---
nav: toc
---

# Context

There are no global variables in the Gentee language. One of the ways to exchange data is a special associative array of strings \(_context_\). Any function can safely add key-value pairs there or get a value by key. In addition, the context has the ability to substitute other existing values from the context. For example, if the pairs _"a": "String A"_ and _"b": "String B"_ has been defined, then _"\#a\# and \#b\#"_ will return _"String A and String B"_. The functions and operators for working with the context are described below.

* [Ctx\( str input \) str](context.md#ctx-str-input-str)
* [CtxGet\( str key \) str](context.md#ctxget-str-key-str)
* [CtxIs\( str key \) bool](context.md#ctxis-str-key-bool)
* [CtxSet\( str key, str val \) str](context.md#ctxset-str-key-str-val-str)
* [CtxSet\( str key, bool b \) str](context.md#ctxset-str-key-bool-b-str)
* [CtxSet\( str key, float f \) str](context.md#ctxset-str-key-float-f-str)
* [CtxSet\( str key, int i \) str](context.md#ctxset-str-key-int-i-str)
* [CtxValue\( str key \) str](context.md#ctxvalue-str-key-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\#** ident | str | The same as _CtxGet\(key\)_, where _ident_ is the context key. |
| **\#\#** str | str | The same as _Ctx\(str\)_. Specify any expression that returns a string. |
| ident **\#=** str | str | The same as _CtxSet\(str key, str s\)_, where _ident_ is the context key. |
| ident **\#=** bool | str | The same as _CtxSet\(str key, bool b\)_, where _ident_ is the context key. |
| ident **\#=** float | str | The same as _CtxSet\(str key, float f\)_, where _ident_ is the context key. |
| ident **\#=** int | str | The same as _CtxSet\(str key, int i\)_, where _ident_ is the context key. |

```go
run str {
  str s = ` #AºB#`
  AºB #= `ººº`
  b #= 71
  CD #= `#AºB# #b# == ` 
  return #CD + #b + ##s
}
// ººº 71 == 71 ººº
```

## Functions

### Ctx\(str input\) str

The _Ctx_ function replaces substrings **\#keyname\#** in _input_ string with the value of the corresponding key, if it exists.

```text
run str {
    CtxSetBool(`qq`, true)
    CtxSetFloat(`ff`, 3.1415)
    CtxSet(`out`, "it is #qq# that PI equals #ff#")
    return Ctx("#out#. #notexist#")
}
// it is true that PI equals 3.1415. #notexist#
```

### CtxGet\(str key\) str

The _CtxGet_ function gets the value of the _key_ key, replaces all occurrences of other keys in it, and returns the resulting string. If the specified key is missing, an empty string is returned.

```text
func init {
   CtxSet(`a1`, `end`)
   CtxSet(`a2`, `=#a1#=`)
   CtxSet(`a3`, `+#a2#+#a1#`)
}

run str {
    init()
    return CtxGet(`a3`)
}
// +=end=+end
```

### CtxIs\(str key\) bool

The _CtxIs_ function returns _true_ if there is a value with the specified key in the context. Otherwise, it returns _false_.

### CtxSet\(str key, str val\) str

The _CtxSet_ function adds a key and a value to the context. If the key already exists, it will be assigned a new value. The function returns the value of the key.

### CtxSet\(str key, bool b\) str

The _CtxSet_ function adds a key and a logical value _b_ to the context. A boolean value will be converted to the string _true_ or _false_. The function returns the value of the key.

### CtxSet\(str key, float f\) str

The _CtxSet_ function adds a key and a floating-point number _f_ to the context. The number will be converted to a string. The function returns the value of the key.

### CtxSet\(str key, int i\) str

The _CtxSet_ function adds a key and an integer _i_ to the context. The number will be converted to a string. The function returns the value of the key.

### CtxValue\(str key\) str

The _CtxValue_ function returns the value of the _key_ key as is. Unlike the **CtxGet** function, it does not replace occurrences of other keys. If the specified key is missing, an empty string is returned.

```text
run str {
    CtxSet(`test`, `?value`)
    CtxSet(`param`, `#test# ==`)
    return CtxValue(`param`) + CtxValue(`nop`) + CtxGet(`param`)
}
// #test# ==?value ==
```

