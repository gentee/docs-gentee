# Compilation and execution

Let's see how to use the Gentee compiler and virtual machine in projects in the **Go** programming language.

## Compilation

To get started, you need to create the *Gentee* structure using the **New** function. This structure will store all information about compiled scripts. You just need to create one instance and compile any number of scripts.

To compile scripts, you need to use the methods **Compile**, **CompileFile**, **CompileAndRun**.
The methods *Compile*, *CompileFile*, in case of successful compilation, return the structure *Exec*, which contains the bytecode. You can save or pass this structure for later execution using the **Run** method. The *CompileAndRun* method immediately after compilation executes the script and returns its result.

```go
package main
import (
    "fmt"
    "log"

    "github.com/gentee/gentee"
)

func main() {
    g := gentee.New()

    exec,_, err := g.Compile("run : print(`Hello, world!`)", "")
    if err != nil {
        log.Fatal(err)
    }
    exec.Run(gentee.Settings{})
    exec,_, err = g.CompileFile("/home/ak/scripts/myscript.g")
    if err != nil {
        log.Fatal(err)
    }
    exec.Run(gentee.Settings{})

    var result interface{}
    result, err = g.CompileAndRun("../torun.g")
    fmt.Println(`Error:`, err, `Result:`, result)
}
```

## Bytecode Execution

The ready byte code of the script is stored in a structure of the **Exec** type. To execute it, call the **Run** method. The parameter of the type [**Settings**] (reference.md#type-settings) allows you to pass command line parameters and specify additional settings for the virtual machine.

```go
package main
import (
    "fmt"
    "log"

    "github.com/gentee/gentee"
)

func main() {
    g := gentee.New()

    exec,_, err := g.CompileFile("myscript.g")
    if err != nil {
        log.Fatal(err)
    }
    var result interface{}
    result, err = exec.Run(gentee.Settings{
        CmdLine: []string{
            "-par1",
            "-o",
            "/home/ak/tmp",
        },
    })
    fmt.Println(`Error:`, err, `Result:`, result)
}
```


