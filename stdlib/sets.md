---
nav: toc
---

# Sets

Operators and functions for working with an array of boolean values \(**set** type\) are described here.

* [arr\( set s \) arr.int](sets.md#arr-set-s-arr-int)
* [set\( arr.int a \) set](sets.md#set-arr-int-a-set)
* [set\( str s \) set](sets.md#set-str-s-set)
* [str\( set s \) str](sets.md#str-set-s-str)
* [Set\( set s, int index \) set](sets.md#set-set-s-int-index-set)
* [Toggle\( set s, int index \) bool](sets.md#toggle-set-s-int-index-bool)
* [UnSet\( set s, int index \) set](sets.md#unset-set-s-int-index-set)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** set | int | Returns the set size. |
| **^** set | set | Returns a new set as logical NOT of the source set. _!s\[i\]_ for each item. |
| set **=** set | set | Assignment operator. |
| set **&=** set | set | Create a clone of the set. The new variable will work with the same data set. |
| set **+=** set | set | Appends a set to a set variable. |
| set **&** set | set | Returns a set that is the intersection of two sets. _left\[i\] && right\[i\]_ for each item. |
| set **\|** set | set | Returns a set that is the union of two sets. _left\[i\] \|\| right\[i\]_ for each item. |
| set **\[** int **\]** | bool | Sets/gets a set value. |

## Functions

### arr\(set s\) arr.int

The _arr_ function converts a _set_ value to an array of integers that contains indexes of _set_ items.

### set\(str s\) set

The _set_ function converts a string to a _set_ value and returns it. The string must only have 1 and 0 characters.

### set\(arr.int a\) set

The _set_ function converts an array of integers to a _set_ value and returns it. The result set will have items with corresponding indexes.

```text
run arr.int {
  set s &= {780, 99, 128, 105, 136}
  arr.int as = arr(s)
  as += 330
  s &= set(as)
  return arr(s) // [99 105 128 136 330 780]
}
```

### str\(set s\) str

The _str_ function converts a _set_ value to a string and returns it. The result string contains only 1 and 0.

### Set\(set s, int index\) set

The _Set_ function adds an index item to the set. It is the same as _s\[index\] = true_. The function returns _s_.

### Toggle\(set s, int index\) bool

The _Toggle_ function adds an index item to the set if the set doesn't have it and otherwise, the function removes the item. It is the same as _s\[index\] = !s\[index\]_. The function returns the previous state - _true_ if the item existed and, otherwise, false.

### UnSet\(set s, int index\) set

The _UnSet_ function removes an index item from the set. It is the same as _s\[index\] = false_. The function returns _s_.

