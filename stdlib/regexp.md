---
nav: toc
---

# Regular expressions

Functions for working with regular expressions are described here.

* [FindFirstRegExp\( str src, str re \) arr.str](regexp.md#findfirstregexp-str-src-str-re-arr-str)
* [FindRegExp\( str src, str re \) arr.arr.str](regexp.md#findregexp-str-src-str-re-arr-arr-str)
* [Match\( str s, str re \) bool](regexp.md#match-str-s-str-re-bool)
* [RegExp\( str src, str re \) str](regexp.md#regexp-str-src-str-re-str)
* [ReplaceRegExp\( str src, str re, str repl \) str](regexp.md#replaceregexp-str-src-str-re-str-repl-str)

## Functions

### FindFirstRegExp\(str src, str re\) arr.str

The _FindFirstRegExp_ function finds the first occurrence of the regular expression _re_ in the specified string _src_. The function returns an array of strings. The first element contains a substring that matches the regular expression, the remaining elements contain values of **(...)** groups, if they are defined in the regular expression.

```go
arr.str a &= FindFirstRegExp(`This45i33s a isi777s inis1i2sg`, `is(\d*)i(\d+)s`)
// a = {`is45i33s`, `45`, `33`}
```

### FindRegExp\(str src, str re\) arr.arr.str

The _FindRegExp_ function finds all occurrences of the _re_ regular expression in the specified string _src_. The function returns an array of arrays. The first element in each array contains a substring that matches the regular expression.

```go
arr.arr.str a &= FindRegExp(`My email is xyz@example.com`, `(\w+)@(\w+)\.(\w+)`)
// a = { { `xyz@example.com`, `xyz`, `example`, `com`} }
a &= FindRegExp(`This is a test string`, `i.`)
// a = { { `is` }, {`is`}, {`in`} }
```

### Match\(str s, str re\) bool

The _Match_ function reports whether the string _s_ contains any match of the regular expression pattern _re_.

```go
bool a = Match(`somethiabng striabnbg`, `a.b`)  // false
a = Match(`somethianbg string`, `a.b`) // true
```

### RegExp\(str src, str re\) str

The _RegExp_ function returns the first occurrence of the regular expression _re_ in the specified line _src_. If no match is found, an empty string is returned.

```go
  str input = "This is a string тестовое значение"
  ret = RegExp(input, `is (.{2})`) + RegExp(input, `е(.+?)е`)
  // isстово
```

### ReplaceRegExp\(str src, str re, str repl\) str

The _FindRegExp_ function replaces matches of the _re_ regular expression with the replacement string _repl. You can specify_ $i _or_ ${i} _in_ repl\* for i-the submatch.

```go
str s = ReplaceRegExp("This is a string", `i(.{2})`, "xyz") 
// Thxyzxyza strxyz
s = ReplaceRegExp(" email is xyz@example.com", `(\w+)@(\w+)\.(\w+)`, "${3}.${2}@zzz")
// email is com.example@zzz
```

