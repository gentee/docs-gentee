# Lexical elements

Source code is UTF-8 encoded. The syntax is specified using Extended Backus-Naur Form.

```text
newline        = 0x0A
unicode_char = /* Unicode code point */
unicode_linechar  = /* Unicode code point except newline */
unicode_letter = /* a Unicode code point classified as "Letter" */
letter        = unicode_letter | "_"
decimal_digit = "0" … "9" 
octal_digit   = "0" … "7" 
hex_digit     = "0" … "9" | "A" … "F" | "a" … "f" 
decimals  = decimal_digit { decimal_digit }
exponent  = ( "e" | "E" ) [ "+" | "-" ] decimals
```

### Comments and character substitution

There are the following types of comments and automatically substitution characters.

`// Single-line comment is here`  
This single-line comment starts with the character sequence `//` and stops at the end of the line.

`/* General comment is here */`  
General comments can appear anywhere. Such comment begins with a forward slash/asterisk combination / _and is terminated by “end comment” delimiter_ /.

`# header`  
At the beginning of the script, you can specify the parameters for use in other programs. Such comments should must be listed one after the other in each line from the beginning of the script. If you do not want to specify '\#' at the beginning of each line, then insert **\#\#\#** before and after the text.

```text
#!/usr/local/bin/gentee
# the first line can be used to run the script on Linux.
###
  desc = Description of the script
  result = ok
  var = value
###
```

**;**  
The new line character is the separating character between expressions and statements. A semicolon is replaced with a new line character. So, you can use semicolons if you want to put several statements on one line.

**:**  
A colon is replaced with an opening curly brace and a closing curly brace is added at the end of the current line.

```text
// These examples are equivalent
if a == 10 : a = b + c; c = d + e 

if a == 10 
{
   a = b + c
   c = d + e
}
```

### Identifiers

Identifiers are names that are used to refer to variables, types, functions, constants etc. An identifier is a sequence of letters and digits. The first character of the identifier must be a letter.

```text
identifier = letter { letter | unicode_digit }
IdentifierList = identifier { identifier }
```

There are some predeclared identifiers and keywords. The following words are reserved and may not be used as identifiers.

#### Keywords

**catch const elif else false for func go if in local recover retry return run struct true try while**

#### Predeclared stdlib types

**arr bool buf char error finfo float int map range set str time trace thread**

### Literals

An integer literal is a sequence of digits representing an integer constant.

```text
decimal = ( "1" … "9" ) { decimal_digit } 
octal = "0" { octal_digit } .
hex = "0" ( "x" | "X" ) hex_digit { hex_digit } 
integer = decimal | octal | hex
float = decimals "." [ decimals ] [ exponent ] | decimals exponent
```

```text
0x34Fab
0722
19023862
0.123e+3
234.e-2
9.7732E-1
0.0177E+2
5e-2
```

A _char_ literal represents an integer value identifying a Unicode code point. You can specify one character or a sequence of characters beginning with a backslash enclosed in single quotes. Multi-character sequences can be like these:

```text
'\r',  '\n',  '\t', '\"', '\'', '\\' 
\xa5 \x2B  (\x + two hex_digit)
\u03B1  (\u + four hex_digit)
\0371  (\0 + three octal_digit)
```

```text
byteVal  = octalStr | hexStr .
octalStr = `\` "0" octal_digit octal_digit octal_digit .
hexStr   = `\` "x" hex_digit hex_digit .
uShort   = `\` "u" hex_digit hex_digit hex_digit hex_digit .
uLong    = `\` "U" hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit .
escapedChar     = `\` ( "a" | "b" | "f" | "n" | "r" | "t" | "v" | `\` | `"` ) 
charLit         = "'" ( unicode_char | uShort | uLong | escapedChar | byteVal | `\'`) "'" .
```

There are two types of string literals. 1. A string in backquotes can contain any characters. If you want to specify a backquote, then you need to double it. 2. A double-quoted string can also contain any characters \(including a line break\), but it has a backslash control character. You can specify the following characters after a backslash:

```text
\a   U+0007 alert or bell  
\b   U+0008 backspace  
\f   U+000C form feed  
\n   U+000A newline  
\r   U+000D carriage return  
\t   U+0009 horizontal tab  
\v   U+000b vertical tab  
\\   U+005c backslash  
\"   U+0022 double quote
```

```text
stringLit         = stringBackQuote | stringDoubleQuote
stringBackQuote   = "`" { unicode_char | "%{" Expression "}" | "${" identifier "}" } "`"
stringDoubleQuote = `"` { unicode_char | uShort | uLong | escapedChar | byteVal | "\{" Expression "}" } `"`
```

You can insert expressions into any type of string. In this case, the result type of expression can be any, if there is a corresponding function that can convert this value to a string. Expressions must be enclosed in curly brackets with the preceding **%** sign \(for backquotes\) or a backslash \(for double quotes\).

```text
`10+20 equals %{10 + 20}. User name is "%{USERNAME}"`
"This is the first line.\r\nThis is \{ `the` + `second`} line."
```

## 

