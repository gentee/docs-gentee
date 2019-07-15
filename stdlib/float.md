---
nav: toc
---

# Float numbers

Operators and functions for working with decimal numbers of **float** type are described here.

* [bool\( float f \) bool](float.md#bool-float-f-bool)
* [Ceil\( float f \) int](float.md#ceil-float-f-int)
* [Floor\( float f \) int](float.md#floor-float-f-int)
* [int\( float f \) int](float.md#int-float-f-int)
* [Max\( float fl, float fr \) float](float.md#max-float-fl-float-fr-float)
* [Min\( float fl, float fr \) float](float.md#min-float-fl-float-fr-float)
* [Round\( float f \) int](float.md#round-float-f-int)
* [Round\( float f, int digit \) float](float.md#round-float-f-int-digit-float)
* [str\( float f \) str](float.md#str-float-f-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| float **+** float | float | Adds two numbers. |
| float **+** int | float |  |
| int **+** float | float |  |
| float **-** float | float | Subtracts second number from the first. |
| float **-** int | float |  |
| int **-** float | float |  |
| float **\*** float | float | Multiplies both numbers. |
| float **\*** int | float |  |
| int **\*** float | float |  |
| float **/** float | float | The division of two numbers. When dividing by zero, an error is returned. |
| float **/** int | float |  |
| int **/** float | float |  |
| float **==** float | bool | Returns true if two numbers are equal and false, otherwise. |
| float **==** int | bool |  |
| float **&gt;** float | bool | Returns true if the first number is greater than the second and false, otherwise. |
| float **&gt;** int | bool |  |
| float **&lt;** float | bool | Returns true if the first number is less than the second and false, otherwise. |
| float **&lt;** int | bool |  |
| float **!=** float | bool | Returns true if two numbers are not equal and false, otherwise. |
| float **!=** int | bool |  |
| float **&gt;=** float | bool | Returns true if the first number is greater than or equal to the second and false, otherwise. |
| float **&gt;=** int | bool |  |
| float **&lt;=** float | bool | Returns true if the first number is less than or equal to the second and false, otherwise. |
| float **&lt;=** int | bool |  |
| **-** float | float | Change the sign of a decimal number. |
| float **=** float | float | Simple assignment operator. |
| float **+=** float | float | Add and assignment operator. |
| float **-=** float | float | Subtract and assignment operator. |
| float **/=** float | float | Divide and assignment operator. |
| float **\*=** float | float | Multiply and assignment operator. |

## Functions

### bool\(float f\) bool

The bool function returns false if the passed parameter is 0.0, otherwise it returns true.

### int\(float f\) int

The _int_ function converts a decimal number to an integer number which is less than or equal to this number.

### str\(float f\) str

The _str_ function converts a decimal number to a string.

### Ceil\(float f\) int

The _Ceil_ function returns the least integer value greater than or equal to _f_.

### Floor\(float f\) int

The _Floor_ function returns the greatest integer value less than or equal to _f_.

### Max\(float fl, float fr\) float

The _Max_ function returns the maximum of two values.

### Min\(float fl, float fr\) float

The _Min_ function returns the minimum of two values.

### Round\(float f\) int

The _Round_ function returns the nearest integer, rounding half away from zero.

```text
   Round(4.5) // 5
   Round(4.1) // 4
   Round(4.9) // 5
```

### Round\(float f, int digit\) float

The _Round_ function rounds _f_ to the specified number of decimal places.

```text
   Round(4.567, 2) // 4.57
   Round(4.111, 1) // 4.1
```

