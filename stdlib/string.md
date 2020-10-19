---
nav: toc
---

# Strings

Operators and functions for working with strings \(**str** type\) are described here.

* [bool\( str s \) bool](string.md#bool-str-s-bool)
* [float\( str s \) float](string.md#float-str-s-float)
* [int\( str s \) int](string.md#int-str-s-int)
* [Find\( str s, str substr \) int](string.md#find-str-s-str-substr-int)
* [Format\( str s, anytype args... \) str](string.md#format-str-s-anytype-args-str)
* [HasPrefix\( str s, str prefix \) bool](string.md#hasprefix-str-s-str-prefix-bool)
* [HasSuffix\( str s, str suffix \) bool](string.md#hassuffix-str-s-str-suffix-bool)
* [Left\( str s, int i \) string](string.md#left-str-s-int-i-str)
* [Lines\( str s \) arr.str](string.md#lines-str-s-arrstr)
* [Lower\( str s \) string](string.md#lower-str-s-str)
* [Repeat\( str s, int count \) str](string.md#repeat-str-s-int-count-str)
* [Replace\( str s, str old, str new \) str](string.md#replace-str-s-str-old-str-new-str)
* [Right\( str s, int i \) string](string.md#right-str-s-int-i-str)
* [Size\( int size, str format \) string](string.md#size-int-size-str-format-str)
* [Split\( str s, str sep \) arr.str](string.md#split-str-s-str-sep-arrstr)
* [Substr\( str s, int off, int length \) str](string.md#substr-str-s-int-off-int-length-str)
* [Trim\( str s, str cutset \) str](string.md#trim-str-s-str-cutset-str)
* [TrimLeft\( str s, str cutset \) str](string.md#trimleft-str-s-str-cutset-str)
* [TrimRight\( str s, str cutset \) str](string.md#trimright-str-s-str-cutset-str)
* [TrimSpace\( str s \) str](string.md#trimspace-str-s-str)
* [Upper\( str s \) string](string.md#upper-str-s-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| str **+** str | str | Merges two strings. |
| **\*** str | int | Returns the length of the string. |
| str **?** | bool | Calls *bool(str)*. |
| **\|** str | str | This unary operator trims whitespace characters in the each line of the string. |
| str **==** str | bool | Returns _true_ if the two strings are equal and _false_, otherwise. |
| str **&gt;** str | bool | Returns _true_ if the first string is greater than the second and _false_, otherwise. |
| str **&lt;** str | bool | Returns _true_ if the first string is less than the second and _false_, otherwise. |
| str **!=** str | bool | Returns _true_ if the two strings are not equal and _false_, otherwise. |
| str **&gt;=** str | bool | Returns _true_ if the first string is greater than or equal to the second and _false_, otherwise. |
| str **&lt;=** str | bool | Returns _true_ if the first line is less than or equal to the second and _false_, otherwise. |
| str **=** str | str | Assignment operator. |
| str **=** int | str | Converts an integer to a string and assigns it to a variable. |
| str **=** bool | str | Assigns "true" or "false". |
| str **+=** str | str | Appends a string to a string variable. |
| str **\[** int **\]** | int | Sets/gets Unicode code by index. |

## Functions

### bool\(str s\) bool

The _bool_ function returns _false_ if the string is empty, "0" or "false", otherwise, it returns _true_.

### float\(str s\) float

The _float_ function converts a string to a number of _float_ type. If the string has the wrong format, an error is returned.

### int\(str s\) int

The _int_ function converts a string to an integer number. If the string has the wrong format, an error is returned.

### Find\(str s, str substr\) int

The _Find_ function returns the index of the first instance of _substr_ in _s_, or -1 if _substr_ is not present in _s_.

### Format\(str s, anytype args...\) str

The _Format_ function formats according to a _s_ specifier and returns the resulting string. There are the following format verbs:

#### General

* **%v** - the value in a default format
* **%%** - a literal percent sign; consumes no value

#### bool

* **%t** -    the word true or false

#### int

* **%b** - base 2
* **%c** - the character represented by the corresponding Unicode code point
* **%d** - base 10. This is the default format for _int_.
* **%o** - base 8
* **%x** - base 16, with lower-case letters for a-f
* **%X** - base 16, with upper-case letters for A-F
* **%U** - Unicode format: U+1234

#### float

* **%e** - scientific notation, e.g. -1.234456e+78
* **%E** - scientific notation, e.g. -1.234456E+78
* **%f** - decimal point but no exponent, e.g. 123.456. You can specify the width and the precision like _%\[width\].\[precision\]f_ - _%8.2f, %.3f, %7f_.
* **%g** - %e for large exponents, %f otherwise. Precision is discussed below. This is the default format for _float_.

#### str

* **%s** - the default format for strings
* **%x** - base 16, lower-case, two characters per byte
* **%X** - base 16, upper-case, two characters per byte

You can specify i-th argument in the format string like this - _Format\("%d %\[1\]d %\[1\]d", 10\)_

```text
arr.int mya = {1,2,3}
time t
Format(`%s %v %v %g %6.2[4]f`, `ok`, mya, Now(t), 99.0 + 1.)
```

### HasPrefix\(str s, str prefix\) bool

The _HasPrefix_ function returns _true_ if the string _s_ begins with _prefix_.

### HasSuffix\(str s, str suffix\) bool

The _HasSuffix_ function returns _true_ if the string _s_ ends with _suffix_.

### Left\(str s, int i\) str

The _Left_ function extracts a given number of characters from the left side of the string _s_.

### Lines\(str s\) arr.str

The _Lines_ function slices _s_ multi-line string into all substrings separated by new line. All substrings are returned as an array of strings.

### Lower\(str s\) str

The _Lower_ function converts a copy of _s_ string to lower case and returns it.

### Repeat\(str s, int count\) str

The _Repeat_ function returns a new string consisting of _count_ copies of the string _s_.

### Replace\(str s, str old, str new\) str

The _Replace_ function returns a copy of the string _s_ with all _old_ strings replaced by _new_ string.

### Right\(str s, int i\) str

The _Right_ function returns a substring of the last _i_ characters of the _s_ string.

### Size\(int size, str format\) str

The _Size_ function returns the rounded size as a string. In the _format_ parameter specify an output pattern for a decimal floating-point number and a string. If _format_ is an empty string, the format *%.2f%s* is used.

``` go
Print( Size(956348901, `%.1f %s `) + Size(62, `%[2]s%.2[1]f `) + Size(123789, ``))
// 912.0 MB B62 120.89KB
```

### Split\(str s, str sep\) arr.str

The _Split_ function slices _s_ string into all substrings separated by _sep_ string. All substrings are returned as an array of strings.

### Substr\(str s, int off, int length\) str

The _Substr_ function returns a substring of the string _s_ with the specified offset and length.

### Trim\(str s, str cutset\) str

The _Trim_ function returns a substring of the string _s_, with all leading and trailing Unicode code points contained in _cutset_ removed.

### TrimLeft\(str s, str cutset\) str

The _TrimLeft_ function returns a substring of the string _s_, with all leading Unicode code points contained in _cutset_ removed.

### TrimRight\(str s, str cutset\) str

The _TrimRight_ function returns a substring of the string _s_, with all trailing Unicode code points contained in _cutset_ removed.

### TrimSpace\(str s\) str

The _TrimSpace_ function returns a substring of the string _s_, with all leading and trailing white space removed.

### Upper\(str s\) str

The _Upper_ function converts a copy of _s_ string to upper case and returns it.

