---
nav: toc
---

# Characters

Operators and functions for working with characters \(**char** type\) are described here.

* [int\( char c \) int](char.md#int-char-c-int)
* [str\( char c \) str](char.md#str-char-c-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| char **+** char | str | Returns a string of two characters. |
| char **+** str | str | Returns a string as the result of adding a string to a character. |
| str **+** char | str | Returns a string as the result of adding a character to the string. |
| char **=** char | char | Assignment operator. |
| str **+=** char | str | Appends a character to the string |
| char **==** char | bool | Returns _true_ if the two characters are equal and _false_, otherwise. |
| char **&gt;** char | bool | Returns _true_ if the first character is greater than the second and _false_, otherwise. |
| char **&lt;** char | bool | Returns _true_ if the first character is less than the second and _false_, otherwise. |
| char **!=** char | bool | Returns _true_ if the two characters are not equal and _false_, otherwise. |
| char **&gt;=** char | bool | Returns _true_ if the first character is greater than or equal to the second and _false_, otherwise. |
| char **&lt;=** char | bool | Returns _true_ if the first character is less than or equal to the second and _false_, otherwise. |

## Functions

### int\( char c \) int

The _int_ function returns the numeric value of a character.

### str\(char c\) str

The _str_ function converts a character to a string and returns this string.

