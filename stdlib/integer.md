---
nav: toc
---

# Integer

Operators and functions for working with integers of **int** type are described here.

* [bool\( int i \) bool](integer.md#bool-int-i-bool)
* [float\( int i \) float](integer.md#float-int-i-float)
* [Max\( int l, int r \) int](integer.md#max-int-l-int-r-int)
* [Min\( int l, int r \) int](integer.md#min-int-l-int-r-int)
* [str\( int i \) str](integer.md#str-int-i-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| int **+** int | int | The addition of two integers. |
| int **-** int | int | Subtract two integers. |
| int **\*** int | int | Multiplication of two integers. |
| int **/** int | int | The division of two integers. When dividing by zero, an error is returned. |
| int **==** int | bool | Returns _true_ if two numbers are equal and _false_, otherwise. |
| int **&gt;** int | bool | Returns _true_ if the first number is greater than the second and _false_, otherwise. |
| int **&lt;** int | bool | Returns _true_ if the first number is less than the second and _false_, otherwise. |
| int **!=** int | bool | Returns _true_ if two numbers are not equal and _false_, otherwise. |
| int **&gt;=** int | bool | Returns _true_ if the first number is greater than or equal to the second and _false_, otherwise. |
| int **&lt;=** int | bool | Returns _true_ if the first number is less than or equal to the second and _false_, otherwise. |
| int **%** int | int | Returns the remainder after dividing two numbers \(modulo operator\). |
| int **\|** int | int | Bitwise OR. |
| int **^** int | int | Bitwise XOR. |
| int **&** int | int | Bitwise AND. |
| int **&lt;&lt;** int | int | Bitwise left shift. |
| int **&gt;&gt;** int | int | Bitwise right shift. |
| **-** int | int | Change the sign of an integer. |
| **^** int | int | Bitwise NOT. |
| int **=** int | int | Simple assignment operator. |
| int **=** char | int | Assigning a character to a variable. |
| int **+=** int | int | Add and assignment operator. |
| int **-=** int | int | Subtract and assignment operator. |
| int **/=** int | int | Divide and assignment operator. |
| int **\*=** int | int | Multiply and assignment operator. |
| int **%=** int | int | Modulus and assignment operator. |
| int **\|=** int | int | Bitwise and assignment operator. |
| int **^=** int | int | Bitwise exclusive OR and assignment operator. |
| int **&=** int | int | Bitwise inclusive OR and assignment operator. |
| int **&lt;&lt;=** int | int | Left shift and assignment operator. |
| int **&gt;&gt;=** int | int | Right shift AND assignment operator. |

## Functions

### bool\(int i\) bool

The _bool_ function returns _false_ if the passed parameter is 0, otherwise it returns _true_.

### float\(int i\) float

The _float_ function converts an integer to a _float_ number.

### Max\(int l, int r\) int

The _Max_ function returns the maximum of two values.

### Min\(int l, int r\) int

The _Min_ function returns the minimum of two values.

### str\(int i\) str

The _str_ function converts an integer to a string.

