# Declarations

### Constant declarations

The constant name can not contain lowercase letters. Constants can be assigned to any expressions. The value of the constant is computed when the constant is first accessed, but the type of the constant is automatically determined at the compilation stage by the type of the assigned expression. Therefore, despite the fact that the type is not specified when defining a constant, type checking is in effect when a constant is used.

```text
ConstDecl      = "const" ( ConstIota | ConstExp )
ConstIota = Expression "{" { IdentifierList newline } "}"
ConstExp = "{" { identifier "=" Expression newline } "}"
```

Constants can be defined in two ways.

1. Specifying an initial value or an expression for each constant.

   ```text
   const {
    MY_ID = 1
    MY_VAL = myFunc( MY_ID + 23)
    CHECK= MY_VAL < 32
   }
   ```

2. Using a common expression with **IOTA**.  Sometimes it is necessary to define a list of constants with values that are computed according to certain rules. In this case, after the **const** keyword, you need to specify one common expression that will be calculated for each constant in this definition. In this expression, you can use the special variable _IOTA_, which is equal to the ordinal index of the constant in the list, starting at zero. Constants should be separated by a space or a new line.

```text
const 0x1 << IOTA {
      FIRST SECOND   // 0x1    0x2
      THIRD                   // 0x4
}
const (IOTA * 2) + 1 {
      MY1    // 1
      MY2   // 3
      MY3   // 5
}
```

### Function declarations

The function declaration consists of two parts - a description of the parameters with the return type and the function body. When you define a function, you must specify the keyword "func", the function name, the parameters to be passed, and the type of the return value. Only the function name is required.

```text
FunctionDecl   = "func" FunctionName [Parameters] [ Result ] Block
FunctionName   = identifier 
Result         = TypeName 
Parameters     = "(" [ ParameterList ] ["..."] ")"
ParameterList  = VarList { "," VarList }
```

```text
func VariadicExample(int i, int s...) int {
    int sum = i*2
    for v in s {
       sum += v
    }
    return sum
}
func MyFunc(int par1 par2) int { 
    int par3 = VariadicExample(3, par1, par2, 4, 5, par1+par2)
    return (par1+par2 +par3)/3 
}
```

The final incoming parameter in a function signature may have a _'...'_ suffix. A function with such a parameter is called _variadic_ function and may be invoked with zero or more arguments for that parameter. You get this parameter as an array of arguments. For example, _int pars..._ means that _pars_ is really _arr.int_ and you can get the i-th argument with _pars\[i\]_.

### Run declaration

The Gentee script must contain a special function without parameters, which is defined using the keyword "run". The script starts by calling this function. The script must have only one definition of "run".

```text
RunDecl = "run" [FunctionName] [ Result ] Block
```

```text
run int {
    int i ret
    while i < 10 {
       ret += myFunc(i++)
    }
    return ret
}
```

