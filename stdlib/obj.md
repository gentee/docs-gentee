# Object

The **obj** type is used to store values of the following types - **int, bool, float, str, arr.obj, map.obj**. If no value is assigned to the object, then it is equal to **nil**. An object can be assigned values of a type that is different from the current one.  
The operators and functions for working with objects are described here.

* [bool\( obj o \) bool](obj.md#bool-obj-o-bool)
* [obj\( bool b \) obj](obj.md#obj-bool-b-obj)
* [obj\( float f \) obj](obj.md#obj-float-f-obj)
* [obj\( int i \) obj](obj.md#obj-int-i-obj)
* [obj\( str s \) obj](obj.md#obj-str-s-obj)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| obj **?** | bool | Calls *bool(obj)*. |

## Functions

### bool\(obj b\) bool

The _bool_ function returns a logical value of the current type. For example, if an object contains a string, the result of calling _bool(str)_ is returned. If the object is not defined, an error is returned.

### obj\(bool b\) obj

The _obj_ function creates an object with the specified logical value.

### obj\(float f\) obj

The _obj_ function creates an object with the specified **float** value.

### obj\(int i\) obj

The _obj_ function creates an object with the specified **int** value.

### obj\(str s\) obj

The _obj_ function creates an object with the specified **str** value.
