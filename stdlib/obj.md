# Object

The **obj** type is used to store values of the following types - **int, bool, float, str, arr.obj, map.obj**. If no value is assigned to the object, then it is equal to **nil**. An object can be assigned values of a type that is different from the current one.  
The operators and functions for working with objects are described here.

* [arr\( obj o \) arr.obj](obj.md#arr-obj-o-arr-obj)
* [bool\( obj o \) bool](obj.md#bool-obj-o-bool)
* [bool\( obj o, bool def \) bool](obj.md#bool-obj-o-bool-def-bool)
* [float\( obj o \) float](obj.md#float-obj-o-float)
* [float\( obj o, float def \) float](obj.md#float-obj-o-float-def-float)
* [int\( obj o \) int](obj.md#int-obj-o-int)
* [int\( obj o, int def \) int](obj.md#int-obj-o-int-def-int)
* [IsNil\( obj o \) bool](obj.md#isnil-obj-o-bool)
* [item\( obj o, int i \) obj](obj.md#item-obj-o-int-i-obj)
* [item\( obj o, str s \) obj](obj.md#item-obj-o-str-s-obj)
* [map\( obj o \) map.obj](obj.md#map-obj-o-map-obj)
* [obj\( arr.typename a \) obj](obj.md#obj-arr-typename-a-obj)
* [obj\( bool b \) obj](obj.md#obj-bool-b-obj)
* [obj\( float f \) obj](obj.md#obj-float-f-obj)
* [obj\( int i \) obj](obj.md#obj-int-i-obj)
* [obj\( map.typename m \) obj](obj.md#obj-map-typename-m-obj)
* [obj\( str s \) obj](obj.md#obj-str-s-obj)
* [Sort\( arr.obj o, cmpobjfunc cmpfunc \) arr.obj](obj.md#sort-arr-obj-o-cmpobjfunc-cmpfunc-arr-obj)
* [str\( obj o \) str](obj.md#str-obj-o-str)
* [str\( obj o, str def \) str](obj.md#str-obj-o-str-def-str)
* [Type\( obj o \) str](obj.md#type-obj-o-str)

## Types

### fn cmpobjfunc(obj, obj) int

The **cmpobjtype** function type is used to compare two objects. Functions of this type are used to sort objects in an array.

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| *obj | int | If the object is _arr.obj_ or _map.obj_, the number of items in the array is returned. Otherwise, it returns 0. |
| obj **?** | bool | Calls *bool(obj)*. |
| obj **=** arr.typename | obj | Assigning an array to an object. |
| obj **=** bool | obj | Assigning a boolean value to an object. |
| obj **=** float | obj | Assigning a decimal number to an object. |
| obj **=** int | obj | Assigning a number to an object. |
| obj **=** map.typename | obj | Assigning an associative array to an object. |
| obj **=** obj | obj | Assignment operator. |
| obj **=** str | obj | Assigning a string to an object. |
| obj **+=** obj | obj | Adding an object to an array of objects. |
| obj **&=** obj | obj | Creates a clone of the object. The new variable will work with the same data set. |
| obj **\[** int/str **\]** | obj | Assign / get the value of an array by index. If the object is not _arr.obj_ or _map.obj_, then an error occurs. |

## Functions

### arr\(obj o\) arr.obj

The _arr_ function returns an array of objects. Object _o_ must be an array, otherwise it returns an error. Calling the function does not create a new array, but returns the current array that contains the _o_ object.

### bool\(obj o\) bool

The _bool_ function returns a logical value of the current type. For example, if an object contains a string, the result of calling _bool(str)_ is returned. If the object is not defined, an error is returned.

### bool\(obj o, bool def\) bool

The _bool_ function returns a logical value of the current type. If the object is not defined, the second parameter is returned.

### float\(obj o\) float

The _float_ function converts an object to a decimal floating-point number. The object must contain a value of **str, int, float** type, otherwise, an error occurs.

### float\(obj o, float def\) float

The _float_ function converts an object to a decimal floating-point number. If the object is not defined, the second parameter is returned. 

### int\(obj o\) int

The _int_ function converts an object to an integer. The object must contain a value of **str, int, float, bool** type, otherwise, an error occurs.

### int\(obj o, int def\) int

The _int_ function converts an object to an integer. If the object is not defined, the second parameter is returned. 

### IsNil\(obj o\) bool

The _IsNil_ function returns _true_ if the object is undefined (equal to **nil**). Otherwise, the function returns _false_.

### item\(obj o, int i\) obj

The _item_ function returns the i-th element of the object. The object must be of **arr.obj** type. If the element is missing, then an empty object is returned.

### item\(obj o, str s\) obj

The _item_ function returns the value of key **s**. The object must be of **map.obj** type. If there is no element, it returns an empty object.

### map\(obj o\) map.obj

The _map_ function returns an associative array of objects. The _o_ object must be an associative array (map), otherwise an error is returned. When the function is called, no new array is created, but the current *map* which contains object _o_ is returned.

### obj\(arr.typename a\) obj

The _obj_ function converts an array of the _arr_ type into an object.

### obj\(bool b\) obj

The _obj_ function creates an object with the specified logical value.

### obj\(float f\) obj

The _obj_ function creates an object with the specified **float** value.

### obj\(int i\) obj

The _obj_ function creates an object with the specified **int** value.

### obj\(map.typename m\) obj

The _obj_ function converts an associative array of the _map_ type into an object.

### obj\(str s\) obj

The _obj_ function creates an object with the specified **str** value.

### Sort\(arr.obj o, cmpobjfunc cmpfunc\) arr.obj

The _Sort_ function sorts an array of objects and returns it. Sorting is done using a function of **cmpobjfunc** type.

``` go
func mySort(obj left, obj right) int {
  if str(left) < str(right) : return -1
  if str(left) > str(right) : return 1
  return 0
}

run str {
  arr a = {"qwr","7","10","ab","тест","абв", "ka"}
  obj o = a
  Sort( arr(o), &mySort.cmpobjfunc )
  ...
}
```

### str\(obj o\) str

The _str_ function converts the object to a string and returns it.

### str\(obj o, str def\) str

The _str_ function converts the object to a string and returns it. If the object is not defined, the second parameter is returned.

### Type\(obj o\) str

The _Type_ function returns the value type of the specified object. The following types may be returned: **int, bool, float, str, arr.obj, map.obj**. If the object is undefined, then **nil** is returned.