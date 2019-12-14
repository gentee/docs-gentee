# Object

The **obj** type is used to store values of the following types - **int, bool, float, str, arr.obj, map.obj**. If no value is assigned to the object, then it is equal to **nil**. An object can be assigned values of a type that is different from the current one.  
The operators and functions for working with objects are described here.

* [bool\( obj o \) bool](obj.md#bool-obj-o-bool)
* [IsNil\( obj o \) bool](obj.md#isnil-obj-o-bool)
* [obj\( bool b \) obj](obj.md#obj-bool-b-obj)
* [obj\( float f \) obj](obj.md#obj-float-f-obj)
* [obj\( int i \) obj](obj.md#obj-int-i-obj)
* [obj\( str s \) obj](obj.md#obj-str-s-obj)
* [str\( obj o \) str](obj.md#str-obj-o-str)
* [Type\( obj o \) str](obj.md#type-obj-o-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| obj **?** | bool | Calls *bool(obj)*. |
| obj **=** obj | obj | Assignment operator. |
| obj **&=** obj | obj | Creates a clone of the object. The new variable will work with the same data set. |

## Functions

### bool\(obj o\) bool

The _bool_ function returns a logical value of the current type. For example, if an object contains a string, the result of calling _bool(str)_ is returned. If the object is not defined, an error is returned.

### IsNil\(obj o\) bool

The _IsNil_ function returns _true_ if the object is undefined (equal to **nil**). Otherwise, the function returns _false_.

### obj\(bool b\) obj

The _obj_ function creates an object with the specified logical value.

### obj\(float f\) obj

The _obj_ function creates an object with the specified **float** value.

### obj\(int i\) obj

The _obj_ function creates an object with the specified **int** value.

### obj\(str s\) obj

The _obj_ function creates an object with the specified **str** value.

### str\(obj o\) str

The _str_ function converts the object to a string and returns it.

### Type\(obj o\) str

The _Type_ function returns the value type of the specified object. The following types may be returned: **int, bool, float, str, arr.obj, map.obj**. If the object is undefined, then **nil** is returned.