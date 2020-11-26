# Encoding

The functions for converting data from one format to another are described here.

* [Json\( obj o \) str](encoding.md#json-obj-o-str)
* [JsonToObj\( str s \) obj](encoding.md#jsontoobj-str-s-obj)
* [StructDecode\( b buf, struct s \)](encoding.md#structdecode-buf-b-struct-s)
* [StructEncode\( struct s \) buf](encoding.md#structencode-struct-s-buf)

## Functions

### Json\( obj o \) str

The _Json_ function converts a variable of *_obj_* type into **json** string.

### JsonToObj\( str s \) obj

The _JsonToObj_ function converts **json** string into a variable of the *_obj_* type.


``` go 
run str {
  return Json(JsonToObj(`{
         "int": 1234,
         "str": "value",
         "float": -45.67,
          "list":[{"on": true},
            "sub 2",
            "sub 3",
            {
                "q": "OK"
            }]
    }`))
}
// Result {"float":-45.67,"int":1234,"list":[{"on":true},"sub 2","sub 3",{"q":"OK"}],"str":"value"}
```

### StructDecode\( buf b, struct s \)

The _StructDecode_ function converts the binary data of a *buf* variable to the field values of the specified structure variable. The binary data must be created with *StructEncode* function.

``` go
  time t
  StructDecode(StructEncode(Now()), t)
```

### StructEncode\( struct s \) buf

The _StructEncode_ function converts a structured variable to binary and stores the result into a *buf* variable. The function saves only fields of the following types: **int, bool, char, float, buf, str**. Fields of other types are skipped.

``` go
struct tmp {
    str head
    int i
}

run str {
  tmp t1 = {head: `HEADER`, i: -356}
  buf bout = StructEncode(t1)
  ...
}
```
