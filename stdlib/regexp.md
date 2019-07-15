---
nav: toc
---

# Regular expressions

Functions for working with regular expressions are described here.

* [FindRegExp\( str src, str re \) arr.arr.str](regexp.md#findregexp-str-src-str-re-arr-arr-str)
* [Match\( str s, str re \) bool](regexp.md#match-str-s-str-re-bool)
* [ReplaceRegExp\( str src, str re, str repl \) str](regexp.md#replaceregexp-str-src-str-re-str-repl-str)

## Functions

### FindRegExp\(str src, str re\) arr.arr.str

The _FindRegExp_ function finds all occurrences of the _re_ regular expression in the specified string _src_. The function returns an array of arrays. The first element in each array contains a substring that matches the regular expression.

```text
arr.arr.str a &= FindRegExp(`My email is xyz@example.com`, `(\w+)@(\w+)\.(\w+)`)
// a = { { `xyz@example.com`, `xyz`, `example`, `com`} }
a &= FindRegExp(`This is a test string`, `i.`)
// a = { { `is` }, {`is`}, {`in`} }
```

### Match\(str s, str re\) bool

The _Match_ function reports whether the string _s_ contains any match of the regular expression pattern _re_.

```text
bool a = Match(`somethiabng striabnbg`, `a.b`)  // false
a = Match(`somethianbg string`, `a.b`) // true
```

### ReplaceRegExp\(str src, str re, str repl\) str

The _FindRegExp_ function replaces matches of the _re_ regular expression with the replacement string _repl. You can specify_ $i _or_ ${i} _in_ repl\* for i-the submatch.

```text
str s = ReplaceRegExp("This is a string", `i(.{2})`, "xyz") 
// Thxyzxyza strxyz
s = ReplaceRegExp(" email is xyz@example.com", `(\w+)@(\w+)\.(\w+)`, "${3}.${2}@zzz")
// email is com.example@zzz
```

