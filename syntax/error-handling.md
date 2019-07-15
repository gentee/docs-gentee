# Error handling

### Try catch statement

By default, if an error was received at the time of the script execution, the script immediately finishes its work. If you want to avoid the termination of the script, you should use the **try** statement. If an error occurs during the execution of the code inside the _try_ block, the control will pass to the  **catch** block, which must be after **try**. After the _catch_ keyword, it is necessary to specify the name of the variable of _error_ type, which will contain information about the error. You can use \[special functions\] \([https://gentee.github.io/stdlib/runtime\#erriderror-err-int](https://gentee.github.io/stdlib/runtime#erriderror-err-int)\) to get the identifier and error text. If you do not remove the error inside _catch_ with **recover** or **retry**, it will be passed on and the script will finish its work.

```text
TryStmt ="try" Block CatchStmt
CatchStmt = "catch" identifier Block
```

```text
run  {
   try {
      myfunc()
      error(101, "Custom error")
   }
   catch err {
      if ErrID(err) != 101:  error( 102, "Error \{ErrText(err)} has occurred in myfunc()")
   } 
}
```

### Recover statement

The **recover** statement is used inside a **catch** block to remove the error. This command removes the error information, the script exits the current _catch_ block and continues execution.

```text
RecoverStmt = "recover"
```

```text
run str {
   try : 10/0
   catch err :  recover
   return "ok"
} 
// ok
```

### Retry statement

The **retry** statement is used inside a **catch** block to restart **try**. This command removes the error information and the script re-executes the corresponding _try_ block.

```text
RetryStmt = "retry"
```

```text
run {
   str fname
   try {
       fname = ReadString("Specify filename: ")
       Println("Beginning of the file: ", str(ReadFile(fname, 0, 50)))
    } catch err {
       Println("ERROR #\{ErrID(err)}: \{ErrText(err)}")
       retry
    }
}
```

## 

