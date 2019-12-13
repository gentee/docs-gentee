# Types

### Type declaration

A type determines a set of values that have the same operations and functions specific for those values. A type is denoted by a type name. A map is a group of elements of one type, indexed by a set of unique string keys. By default, _arr_ and _map_ arrays consist of strings, but you can specify any nested types by separating them with a dot. Note that variables of types **arr**, **map**, **buf**, **set**, **obj** and types that has been defined with **struct**, unlike other types, are passed by reference, not by value. This means that if you change the value of this parameter inside the function, you will change the original variable.

```go
TypeName  = identifier { "." identifier }
```

The Gentee language predeclares the following types.

**arr bool buf char error finfo float int map obj range set str time trace thread**

| Name | Description | Values | Initial value |
| :--- | :--- | :--- | :--- |
| **int** | 64-bit integer type | -9223372036854775808 .. 9223372036854775807 | 0 |
| **float** | 64-bit double | 2.22 E–308 ..    1.79 E+308 | 0.0 |
| **bool** | boolean type | _true_ or _false_ | false |
| **str** | string | a sequence of bytes | empty string |
| **char** | Unicode character | Unicode code point int32 | space |
| **arr** | array | array of elements | empty array of strings |
| **map** | associative array | associative array of elements | empty associative array of strings |
| **buf** | array of bytes | array of uint8 | empty array |
| **set** | set of bool | array of uint64 with 1 bit per value | empty set |
| **obj** | object | int, bool, float, str, arr.obj, map.obj | nil |

```go
arr.map.int a
map.arr.str b   // the same as map.arr b
map.bool c
arr.int  d
```

### Type casting

There is no automatic type casting in Gentee . For basic types, there are functions for converting from one type to another, their names are the same as the name of the resulting type.

|  | int | bool | str | char | float |
| :--- | :--- | :--- | :--- | :--- | :--- |
| int |  | int\(false\) | int\("-23"\) | int\('A'\) | int\(3.24\) |
| bool | bool\(1\) |  | bool\("0"\) |  | bool\(1.1\) |
| str | str\(20\) | str\(false\) |  | str\('z'\) | str\(5.662\) |
| char |  |  |  |  |  |
| float | float\(10\) |  | float\("-2E-34"\) |  |  |

```go
int(false) // = 0           
int(true) // = 1    
bool(0) // = false  
bool(0.) // = false  
bool(integer except zero) // = true    
bool("")  bool("0") bool("false") //=false
bool("not empty, zero or false string")   //=true
```

### Type definition

You can define a structure type by using the **struct** keyword. Specify a type name after the keyword, and list the field types and names inside the curly braces. All fields in a variable of a structured type are automatically initialized. All variables of these types are passed by reference, rather than by value, when passed to functions. To assign or get a field value, specify its name after the dot.

```go
structDecl = "struct" identifier "{" FieldDecl { newline  FieldDecl } "}"
FieldDecl = TypeName identifier
FieldExpr = PrimaryExpr "." identifier
```

```go
struct my : int ID; str name
struct myStruct {
      int ID
      my myval
      arr st_arr
      map.int st_map
}
run int {
    myStruct ms
    ms.ID = 20
    return ms.ID * 2
}
```

### Function type

The Gentee language allows you to work with function identifiers. You can get the ID of the function, pass it as a parameter and call the corresponding function. To work with function identifiers, you must define a function type using the **fn** keyword and specify the types of parameters and return value. To get the function ID, specify **&function\_name.fn\_type**. The function identifier can be passed in parameters or assigned to a variable of the corresponding _fn_ type. To call a function by its identifier, it is sufficient to specify the variable name and parentheses with parameters, as when calling a function by name.

The function identifier does not apply to the following functions:
* Built-in functions.
* Functions with a variable number of parameters.
* Functions with optional variables.

```go
fnDecl = "fn" FnName [FnParameters] [ TypeName ]
FnName = identifier
FnParameters     = "(" [ FnParameterList ] ")"
FnParameterList  = TypeName { [","] TypeName }
FnIdent = "&" FuncName "." FnName
```

```go
fn bin( int int ) int
func add( int i, int j ) int : return i + j
func sub( int i, int j ) int : return i - j
func mybin(int i j, bin f ) int : return j + f(i, j)

run int {
  bin isub = &sub.bin
  return mybin(1, 2, &add.bin) + mybin(3, 7, isub)
}
```

