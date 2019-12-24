# Object

The **obj** type is used to store values of the following types - **int, bool, float, str, arr.obj, map.obj**. If no value is assigned to the object, then it is equal to **nil**. An object can be assigned values of a type that is different from the current one.  
The operators and functions for working with objects are described here.

* [bool\( obj o \) bool](obj.md#bool-obj-o-bool)
* [float\( obj o \) float](obj.md#float-obj-o-float)
* [int\( obj o \) int](obj.md#int-obj-o-int)
* [IsNil\( obj o \) bool](obj.md#isnil-obj-o-bool)
* [obj\( arr.typename a \) obj](obj.md#obj-arr-typename-a-obj)
* [obj\( bool b \) obj](obj.md#obj-bool-b-obj)
* [obj\( float f \) obj](obj.md#obj-float-f-obj)
* [obj\( int i \) obj](obj.md#obj-int-i-obj)
* [obj\( map.typename m \) obj](obj.md#obj-map-typename-m-obj)
* [obj\( str s \) obj](obj.md#obj-str-s-obj)
* [str\( obj o \) str](obj.md#str-obj-o-str)
* [Type\( obj o \) str](obj.md#type-obj-o-str)

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
| obj **&=** obj | obj | Creates a clone of the object. The new variable will work with the same data set. |
| obj **\[** int/str **\]** | obj | Assign / get the value of an array by index. If the object is not _arr.obj_ or _map.obj_, then an error occurs. |

## Functions

### bool\(obj o\) bool

The _bool_ function returns a logical value of the current type. For example, if an object contains a string, the result of calling _bool(str)_ is returned. If the object is not defined, an error is returned.

### float\(obj o\) float

The _float_ function converts an object to a decimal floating-point number. The object must contain a value of **str, int, float** type, otherwise, an error occurs.

### int\(obj o\) int

The _int_ function converts an object to an integer. The object must contain a value of **str, int, float, bool** type, otherwise, an error occurs.

### IsNil\(obj o\) bool

The _IsNil_ function returns _true_ if the object is undefined (equal to **nil**). Otherwise, the function returns _false_.

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

### str\(obj o\) str

The _str_ function converts the object to a string and returns it.

### Type\(obj o\) str

The _Type_ function returns the value type of the specified object. The following types may be returned: **int, bool, float, str, arr.obj, map.obj**. If the object is undefined, then **nil** is returned.