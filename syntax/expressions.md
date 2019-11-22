# Expressions

The expression returns a value by applying operators and functions to operands. An operand may be a literal, an identifier denoting a constant, variable, or function, or a parenthesized expression. To call a function, specify its name and list the parameters in parentheses separated by comma. Parameters can also be expressions. In addition, you can set the first parameter before the function and separate it by a dot. This helps to more clearly indicate the sequence of function calls.
```go
(b*c).func3(d).func2(a).func1(10)
"my string".Upper().TrimRight("g")
// the same as
func1(func2(func3( b*c, d ), a), 10)
TrimRight(Upper("my string"), "g")
```

```text
Operand     = Literal | OperandName | "(" Expression ")" | GoStmt
Literal     = BasicLiteral
constLit    = "true" | "false"
BasicLiteral    = float | integer | stringLit | constLit | charLit
OperandName = identifier | EnvVariable | FnIdent
PrimaryExpr = Operand | FuncName Arguments | Expression "." FuncName Arguments | IfOp | 
              IndexExp | FieldExpr
OptionalArgs = identifier ":" Expression { "," identifier ":" Expression }
Arguments    = "(" [ ExpressionList ] [ OptionalArgs ] ")" 
ExpressionList = Expression { "," Expression } 
Expression = UnaryExpr | Expression binaryOp Expression | OperandName assignOp Expression
UnaryExpr  = PrimaryExpr | unaryOp UnaryExpr | incOp OperandName | OperandName incOp 
binaryOp  = "||" | "&&" | relOp | mathOp | assignOp | rangeOp
relOp     = "==" | "!=" | "<" | "<=" | ">" | ">=" 
mathOp     = "+" | "-" | "|" | "^" | "*" | "/" | "%" | "<<" | ">>" | "&" | 
unaryOp   = "-" | "!" | "^" | "*" | "#" | "##"
incOp = "++" | "--" 
rangeOp = ".."
assignOp = "=" | "+=" | "-=" | "|=" | "^=" | "*=" | "/=" | "%=" | "<<=" | ">>=" | "&=" | "#="
IfOp = "?" "(" Expression "," Expression "," Expression ")"
```

When calculating the logical operators "&&" \(AND\) and "\|\|" \(OR\), the right operand is evaluated optionally. For example, in the cases of `false && myFunc()` and `true || myFunc ()`, the myFunc function will not be called.

Assignment operators are binary operators that return an assigned value. Therefore, assignment operators can be used within expressions.

```go
int i j k
i = j = 5+(k=60/5)*2
return (k+j)*2 + i   // 111
```

### Operator precedence

As a rule, all statements are executed from left to right, but there is such a concept as statement priority. If the next statement has a higher priority, the statement with a higher priority is executed first. For example, multiplication has a higher priority and 4 + 5  _2 is 14, but if we use parentheses, \( 4 + 5 \)_  2 is 18.

| Operator | Type | Associativity |
| :--- | :--- | :--- |
| The highest priority |  |  |
| \(   \)  \[   \] |  | Left to right |
| -   ^   \#   \#\#   \*   ++   -- | Unary prefix | Right to left |
| ? | Unary postfix | Right to left |
| ! | Unary prefix | Right to left |
| ++   -- | Unary postfix | Left to right |
| /   %   \* | Binary | Left to right |
| +   - | Binary | Left to right |
| &lt;&lt;   &gt;&gt; | Binary | Left to right |
| & | Binary | Left to right |
| ^ | Binary | Left to right |
| \| | Binary | Left to right |
| ==   !=   &lt;   &lt;=   &gt;   &gt;= | Binary | Left to right |
| \|\| | Binary | Left to right |
| && | Binary | Left to right |
| \#= | Binary | Left to right |
| =   +=   -=   \*=   /=   %=   &lt;&lt;=   &gt;&gt;=   &=   ^=   \|= | Binary | Right to left |
| .. | Binary | Left to right |
| The lowest priority |  |  |

Parentheses \(\) change the order in which expressions are evaluated. Increment operations ++ and -- can be occurred either in the prefix or in the postfix notation.

### Conditional operator "?"

Conditional operator "?" is similar in its work to the "if" statement, but can be used inside an expression. The conditional operator has three operand expressions. The operands are enclosed in parentheses and separated by commas, at the beginning the value of the first logical expression is evaluated. If the value is true, the second expression is evaluated and the resulting value is the result of the conditional operator. Otherwise, the third operand is evaluated and its value is returned.

```go
if a >= ?( x, 0xFFF, ?( y < 5 && y > 2, y, 2*b )) + 2345
{
     r = ?( a == 10, a, a + b ) 
}
```

### Arrays and structures initialization

When defining variables of the type _arr_, _set_, _buf_ or _map_, you can immediately assign array elements. You can also specify the field values of structural type variables. Values are listed separated by commas or line breaks. You can specify expressions as a value. When initializing an associative array _map_, you must specify the key as a string and the value after a colon. If the elements of the array are other arrays, they are also initialized using braces. When initializing structure fields, you must specify the key as an identifier and a colon-separated value. A variable of **buf** type can be initialized by a combination of the values of the **int**, **str**, **char**, **buf** types.

```text
DelimInit = "," | newline
ArrInit = "{" VarInit {DelimInit VarInit} "}"
BufInit = "{" Expression {DelimInit Expression} "}"
MapInit = "{" Expression ":" VarInit { DelimInit Expression ":" VarInit  }  "}"
SetInit = "{" Expression {DelimInit Expression} "}"
StructInit = "{" identifier ":" VarInit { DelimInit identifier ":" VarInit  }  "}"
VarInit = ArrInit | BufInit | MapInit | StructInit | SetInit | Expression
```

```go
mystruct my = {ID: 20, name: "some text"}
buf a = {250+5, '1', 'A', "test", 0}
map.arr.int ret = {"key1": {0, 1 }, `key2`:{ 2, 3 } }
arr.map ret = { {"test": "value 1"}
                {`next`:"value 2"} }
arr.bool mb = : true, false, true
map  my = {"key1": GetVal(1), "key2": GetVal(2)}
set s &= {1, 0, 45, myintval, MYCONST}
```

### Index Expression

Indexing allows you to get or set a specific element of a variable by its index. The index is a position of some element inside of the specified variable. Gentee has zero-based indexing \(excepting **map**\), meaning that the first element has the index zero, the second element has the index one, etc. The following types support indexing:

* **str**. The index must be of the **int** type and less than the length of the string. If the index is out of range, a run-time error occurs. The type of the result is **char**.
* **buf**. The index must be of the **int** type and less than the length of the array. If the index is out of range, a run-time error occurs. The type of the result is **int** but 0 &lt;= result value &lt;= 255.
* **arr**. The index must be of the **int** type and less than the length of the array. If the index is out of range, a run-time error occurs. The type of the result is the same as the type of array's elements.
* **map**. The index must be of the **string** type. If a value is obtained, the map must have the element with this key. If there is not the such index, a run-time error occurs. The type of the result is the same as the type of map's elements.
* **set**. The index must be of the **int** type and less than 64000000. If the index is out of range, a run-time error occurs. The type of the result is the boolean value.

If _array_ or _map_ consists of arrays, then you can sequentially apply the index expression.

```text
IndexExp = PrimaryExpr "[" Expression "]" { "[" Expression "]" }
```

```go
str temp = `0123`
temp[1] = temp[3]  // result `0323`
arr ain
ain += `test`
temp = ain[0]
map mymap
mymap["mykey"] = "myvalue"
arr.map amap
amap += mymap
amap[0]["mykey"] = "new value"
```

### Assignment Expressions

There is an assignment operator **=** for all types in the Gentee language. When you use assignment for **buf, arr, map, set**, and all structure types, you will get copies of the data. Consider an example

```go
arr a1 = {`A`, `B`, `C`}
arr a2 = a1
a2 += `D`
a1[0] = `Z`
//  a1 = `Z`, `B`, `C`
//  a2 = `A`, `B`, `C`, `D`
```

When assigning _a2 = a1_ we got a copy of the array _a1_. Actions on arrays will not affect each other in any way. Sometimes making copies of large objects can slow down program execution. For example, if a function returns some structure that you want to work with further, then there is no point in creating its copy. To resolve such situations, there is another assignment operator **&=** for types **buf, arr, map, set** and all structure types. This operator does not copy data into a variable, but creates a clone of this data. In this case, the data remains in a single copy.

```go
arr a1 = {`A`, `B`, `C`}
arr a2 &= a1
a2 += `D`
a1[0] = `Z`
//  a1 = `Z`, `B`, `C`, `D`
//  a2 = `Z`, `B`, `C`, `D`
```

```go
time t
t &= Now()  // it is better than t = Now()
```

### Context

There are no global variables in Gentee. Instead, there is an associative array _map.str_, which is readable and writable from any functions and streams. In addition to storing data as a key-value, the context can also recursively replace keys in strings of the form _"\#key\_name\# \#another\_key\_name\#"_. All [context functions](https://gentee.github.io/stdlib/context) are described in the standard library. Here we consider only operators.

* Unary operator **\#\# str** recursively replaces keys with their values in the passed string and returns the result. 
* Unary operator **\# key** works similarly to the **\#\#** operator, but it needs to pass the name-identifier of the context key.
* The **key \#= value** operator writes the _key_ key with the specified value into the context. If the value is of type _int, bool, float_ instead of type _str_, it will be converted to a string.

```go
func ooops() {
    AB #= `oops`
}
run str {
    AB #= `test`
    CD #= `#AB# - `    // don't replace #AB#.  CD = #AB# - 
    E #= #AB           // get #AB#. E = test
    ooops()            // change AB
    val #= 10
    return #CD + #E + ##` #val# == 10`
}
// Result:  oops - test 10 == 10
```

