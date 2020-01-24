# Encoding

The functions for converting data from one format to another are described here.

* [Json\( obj o \) str](encoding.md#json-obj-o-str)
* [JsonToObj\( str s \) obj](encoding.md#jsontoobj-str-s-obj)

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
