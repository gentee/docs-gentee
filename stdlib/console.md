---
nav: toc
---

# Console

Functions for working with a console described here.

* [Print\( anytype par... \) int](console.md#print-anytype-par-int)
* [Println\( anytype par... \) int](console.md#println-anytype-par-int)
* [ReadString\( str text \) str](console.md#readstring-str-text-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\|\|** str | int | This unary operator writes a string to standard output but it trims whitespace characters in the each line before printing. Returns the number of bytes written. |

```text
run {
   ||`One
      Two
      Three
      `
}
/* It prints
One
Two
Three
*/
```

## Functions

### Print\(anytype par...\) int

The _Print_ function formats using the default formats for operands of any types and writes to standard output. Spaces are added between operands when neither is a string. _Print_ returns the number of bytes written.

### Println\(anytype par...\) int

The _Println_ function formats using the default formats for operands of any types and writes to standard output. Also, it writes a new line character to standard output at the end. Spaces are always added between operands. _Println_ returns the number of bytes written.

### ReadString\(str text\) str

The _ReadString_ function reads the standard input until the first occurrence of '\n' \(Enter key\). It returns a string containing the data up to. If the _text_ parameter is not empty, the function prints this text before reading input.

