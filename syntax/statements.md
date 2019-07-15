# Statements

A block is a sequence of declarations and statements within curly braces. Blocks can be nested into each other.

```text
Block = "{" StatementList "}" .
StatementList = { Statement newline } .
Statement = ReturnStmt | IfStmt | Expression | WhileStmt | VarDeclaration | ForStmt | 
            LocalDecl | BreakStmt | ContinueStmt | SwitchStmt | GoStmt | TryStmt | 
            RecoverStmt | RetryStmt
```

### Variable declarations

Any function variable must be described before it can be used. A variable declaration creates one or more variables and assign to each an initial value. A variable can be defined in any block. The scope of the variable extends to the block in which it is defined and to all nested blocks. You cannot create variables with the name of existing functions and "visible" variables. Also, the variable name must contain at least one lowercase letter, because uppercase names are used for constants. A variable declaration begins by specifying its type. There are two types of initialization - you can define a single variable with a value assigned to it or several variables of the same type with default initialization.

```text
VarDeclaration = VarAssign | VarList
VarList = TypeName ["?"] IdentifierList
VarAssign = TypeName ["?"] identifier "=" | "&=" VarInit
```

```text
int x y myVal
int z = myFunc(x) + y + 10
arr a &= b
```

You can define the **optional parameters-variables** by specifying **?** after the variable type. If you initialize the optional parameter using the assignment operator **=** or **&=**, it will be the default value if the parameter is not defined when the function is called.  
In order to pass an optional parameter when calling the function, it is necessary to specify the variable name and its value separated by a colon. Optional parameters are specified after the obligatory parameters.

```text
func mul(int i) int {
      int ? j = 10
      return i*j
}

run int {
      return mul(7) + mul(5, j: 5)  // 70+25
}
```

### If statement

The **"if"** statements begin with "if", they can have one or more "elif" blocks and end with "else". The statement sequentially evaluates the condition for each branch and if the condition is true, then the corresponding block executes. In this case, the remaining branches are skipped, the statement ends and the control is passed to the next command. If all branch conditions are false, then, if present, the "else" branch is executed.

```text
IfStmt = "if" Expression Block [{ "elif" Expression Block }][ "else" Block ]
```

```text
if a == 11 {
    b = 20
} else {
    c = a+b
}
if x > y && isOK { 
     x = 1 
} elif a > 1 {
   x++
} elif b < 10 {
    b = a
} else {x = 0}
```

### While statement

The **"while"** statement is a simple loop. It specifies the repeated execution of a block as long as a boolean condition evaluates to true. If the condition is false the first time through the loop, the statements inside the loop are never executed.

```text
WhileStmt = "while" Expression Block
```

```text
a = 0
while a < 5 {
   с += a
   a++
}
```

### For statement

The **"for"** statement is used to iterate through all the elements of the specified object. The object must be of a type that supports indexing such as **arr**, **map**, **str**, **buf**, **set**, **range of integers**. For each entry **for** assigns iteration values to corresponding iteration variables if present and then executes the block. You must specify the name of the variable for iteration values and, optionally, the name of the variable for the index value.  
If you want to iterate through a range of integer numbers, use the syntax **from..to** as the object, where _from_ and _to_ are values of the integer type. This will iterate through all the numbers between _from_ and _to_, including the extreme values. The initial value can be greater than the final value, in this case, the iteration value will be decreased.

```text
ForStmt = "for" identifier [, identifier] "in" Expression Block
```

```text
str dest
for ch, i in `strΔ` {
   dest += "\{i}\{ch}"
}
int sum
for i in 0..100 : sum += i
```

### Switch statement

The **"switch"** statement allows you to perform different operations in case an expression has different values. The **switch** keyword is followed by the initial expression that is calculated and stored as the switch value. The switch value can be of type **int, float, char, str**. Then you enumerate **case** statement in curly braces with all possible values and the source code that should be executed. One case can have several possible values separated with a comma in case of which it will be executed. After executing the case block with the matching value, the program goes to the statement coming after switch. The rest of case blocks are not checked.

If you want to execute some operations in case none of the case blocks is executed, insert the **default** construction at the end of switch. The default statement can appear only once and should come after all case statements.

```text
SwitchStmt = "switch" Expression newline CaseStmt { CaseStmt } [ "default" Block ]
CaseStmt = "case" Expression {, Expression } Block
```

```text
int i = 67
int j
switch i+3 
case 20,10,5 {
  i +=10
}
case j,20+50,80 {
  i -=10
}
default: i *= 2
```

### Local functions

You can define the **local** functions within the **func** functions. Local functions can accept parameters and return values. Local functions do not support a variable number of arguments. To return from a local function, you must use the **return** statement. In local functions, you can access external variables and parameters that have been defined above.

```text
LocalDecl   = "local" FunctionName [Parameters] [ Result ] Block
```

```text
run int {
    int i
    local loc(int step) int {
          return (i += 2)+step
    }
    return loc(1) + loc(2)*loc(3)
} 
// result: 57
```

### Return statement

A "return" statement terminates the execution of the current function, and optionally provides a result value. If a function doesn't have a result type, a "return" statement must not specify any result value. You can use "return" statement in any nested block.

```text
ReturnStmt = "return" [ Expression ]
```

```text
func mul2(int i) int { return i*2}
```

### Break statement

The **"break"** statement terminates **switch/case** statement or the execution of the loop \(**for** and **while**\). **break** is likely to be located within nested blocks. If a program contains several nested loops, break will exit the current loop.

```text
BreakStmt = "break"
```

```text
while b > c {
   if !myfunc( b ) {
      break   
   }
   b++
}
```

### Continue statements

The "continue" statement may occur within loops \(**for** and **while**\) and attempts to transfer control to the loop expression, which is used to increment or decrement the counter \(for _for_ or to the conditional expression for _while_; moreover, the execution of the loop body is not completely executed. The instruction executes only the most tightly enclosing loop, if this loop is nested.

```text
ContinueStmt = "continue"
```

```text
for i in 0..100 {
   if i > 10 && i < 20 {
      continue 
   }
   a += i // The given expression is not evaluated if i>10 and i<20
}
```

## 

