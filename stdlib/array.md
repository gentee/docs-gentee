---
nav: toc
---

# Array

Operators and functions for working with arrays \(**arr** type\) are described here. **arr.typename** means that you can specify any type name but in the case of the binary operator this type must be the same in both arrays.

* [Join\( arr.str a, str sep \) str](array.md#join-arr-str-a-str-sep-str)
* [Sort\( arr.str a \) arr.str](array.md#sort-arr-str-a-arr-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** arr.typename | int | Returns the number of elements in the array. |
| arr.typename **=** arr.typename | arr.typename | Assignment operator. |
| arr.typename **&=** arr.typename | arr.typename | Creates a clone of the array. The new variable will work with the same data set. |
| arr.str **+=** str | arr.str | Adds a string to an array of strings. |
| arr.int **+=** int | arr.int | Adds an integer number to an array of integer numbers. |
| arr.bool **+=** bool | arr.bool | Adds a Boolean value to an array of Boolean values. |
| arr.arr.typename **+=** arr.typename | arr.arr.typename | Adds an array to an array of arrays. |
| arr.map.typename **+=** map.typename | arr.map.typename | Adds a map to an array of maps. |
| arr.typename **\[** int **\]** | typename | Sets/gets an array value by index. |

## Functions

### Join\(arr.str a, str sep\) str

The _Join_ function joins strings of the array. The separator string _sep_ is placed between strings in the resulting string.

### Sort\(arr.str a\) arr.str

The _Sort_ function sorts an array of strings in increasing order and returns it.

