# Include and import

### Include and import declarations

The **include** declaration imports all types, functions and constants from the specified files and their included files.

The **import** declaration imports only public types, functions and constants from the specified files and their included files. Public objects are defined using the **pub** keyword.

```text
stringConst         = "`" { unicode_char } "`" | stringDoubleConst
stringDoubleConst = `"` { unicode_char | uShort | uLong | escapedChar | byteVal } `"`
importDecl = "import" "{" {stringConst newline} "}"
includeDecl = "include" "{" {stringConst newline} "}"
```

Consider the visibility of objects as a table. Let there be two files.

```text
// a.g can include or import b.g
func afunc(i int) : return i*2
pub func apubfunc(i int) : return i*3

// b.g 
func bfunc(i int) : return i*4
pub func bpubfunc(i int) : return i*5
```

Let the _c.g_ file can import or include _a.g_ file. You can see what functions are visible in _c.g_ in different situations.

|  | include a   a includes b | include a   a imports b | import a   a includes b | import a   a imports b |
| :--- | :--- | :--- | :--- | :--- |
| afunc | visible | visible |  |  |
| apubfunc | visible | visible | visible | visible |
| bfunc | visible |  |  |  |
| bpubfunc | visible |  | visible |  |

### Pub declaration

The **pub** declaration marks the next function, type or constants as public. They can be imported with **import** declaration.

```text
pubDecl = "pub"
objects = [pubDecl] (structDecl | FnDecl | ConstDecl | FunctionDecl)
```

The **pub** keyword indicates that the next function, constants, or structure will be passed when the file is imported.

```text
pub const IOTA {  // public constants. Visible when include or import
    MY1
    MY2
}

const IOTA*2 {  // private constants. Visible only when include
    MY3
    MY4
}
```

