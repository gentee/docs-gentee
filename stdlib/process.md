---
nav: toc
---

# Process

Operators and functions for working with processes and applications are described here. The _Args_ and _ArgCount_ functions work with any command line format. For the correct operation of other _Arg..._ functions, the command line must have the following format.

```go
CmdLine = [ CmdOptions ] ["-"] [ CmdParameters ]
CmdParameters = { CmdParameter }
CmdParameter = ParamWithoutSpace | "Param With Spaces" | 'Param With Spaces'
CmdOptions = {CmdOption}
CmdOption = "-" | "--" {letter} [ CmdOptionValue | CmdOptionValues ]
CmdOptionValue = "=" | ":" CmdParameter
CmdOptionValues = " " CmdParameters
```

```text
-p="my value" --flag - one two three
-i:10 -n:Bob "one par" two three
--ext "*.txt" .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
```

* [Arg\( str name \) str](process.md#arg-str-name-str)
* [Arg\( str name, str def \) str](process.md#arg-str-name-str-def-str)
* [Arg\( str name, int def \) int](process.md#arg-str-name-int-def-int)
* [ArgCount\(\) int](process.md#argcount-int)
* [Args\(\) arr.str](process.md#args-arr-str)
* [Args\( str name \) arr.str](process.md#args-str-name-arr-str)
* [ArgsTail\(\) arr.str](process.md#argstail-arr-str)
* [IsArg\( str name \) bool](process.md#isarg-str-name-bool)
* [Open\( str path \)](process.md#open-str-path)
* [OpenWith\( str app, str path \)](process.md#openwith-str-app-str-path)
* [Run\( str cmd, str params... \)](process.md#run-str-cmd-str-params)
* [SplitCmdLine\( str cmdline \) arr.str](process.md#splitcmdline-str-cmdline-arr-str)
* [Start\( str cmd, str params... \)](process.md#start-str-cmd-str-params)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **$** command line |  | Executes the command line. |
| str = **$** command line |  | Executes the command line and returns its output. |

## Functions

### Arg\(str name\) str

The _Arg_ function returns the value of the parameter with the specified name. If the parameter was not specified at the start of the script, an empty string will be returned. You can omit the initial character **-** in the _name_ parameter.

### Arg\(str name, str def\) str

The _Arg_ function returns the value of the parameter with the specified **name**. If the parameter was not specified at the start of the script, **def** will be returned. You can omit the initial character **-** in the _name_ parameter.

### Arg\(str name, int def\) int

The _Arg_ function returns the numeric value of the parameter with the specified **name**. If the parameter was not specified at the start of the script, **def** will be returned. You can omit the initial character **-** in the _name_ parameter.

### ArgCount\(\) int

The _ArgCount_ function returns the number of command line parameters with which the script was run.

### Args\(\) arr.str

The _Args_ function returns a list of all command-line parameters and options with which the script has been run.

### Args\(str name\) arr.str

The _Args_ function returns a list of parameter values named **name**. You can omit the initial character **-** in the _name_ parameter.

```text
// --ext .txt .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
list = Args(`--ext`) 
// list == [.txt, .js, .html]
```

### ArgsTail\(\) arr.str

The _ArgsTail_ function returns the list of command line parameters after the options. You can explicitly specify the beginning of such parameters with **-**.

```text
// --ext .txt .js .html -o=/home/ak/dest /home/ak/in1 /home/ak/in2
list = ArgsTail() // list == [/home/ak/in1, /home/ak/in2]

// -i=false - val0 -value1 "value 2" 
list = ArgsTail() // list == [val0, -value1, value 2]
```

### IsArg\(str name\) bool

The _IsArg_ function returns _true_ if the command line has an option with the specified name. Otherwise, it returns _false_. You can omit the initial character **-** in the _name_ parameter.

### Open\(str path\)

The _Open_ function opens a file, directory, or URI using the OS's default application for that object type. Don't wait for the open command to complete.

### OpenWith\(str app, str path\)

The _OpenWith_ function opens a file, directory, or URI using the specified application. Don't wait for the open command to complete.

### Run\(str cmd, str params...\)

**Optional parameters**

* **buf stdin** - the buffer that will be passed to the application as standard input.
* **buf stdout** - the buffer into which the standard output of the application will be written.
* **buf stderr** - the buffer into which the standard error output of the application will be written.

The _Run_ function starts the specified _cmd_ program with parameters and waits for it to finish. Additionally, you can override the standard input and output.

```go
    buf dirout
    Run("dir", stdout: dirout)
    Run("bash", stdin: buf(
      |`echo "dirs"
        #comment    
        echo "%{str(dirout)}"`
    ))
```

### SplitCmdLine\(str cmdline\) arr.str

The _SplitCmdLine_ function parses the input string with command line parameters and returns an array of parameters.

```go
run str {
    return SplitCmdLine(`param1 "second par" "qwert\"y" 100 'oo ps'
-lastparam`).Join(`=`)
}
// returns param1=second par=qwert"y=100=oo ps=-lastparam
```

### Start\(str cmd, str params...\)

**Optional parameters**

* **buf stdin** - the buffer that will be passed to the application as standard input.

The _Start_ function starts the specified program _cmd_ with parameters and runs the script further. Additionally, you can pass the buffer as standard input.

```go
    Start("echo", "hello, world!")
    Start("bash", stdin: buf(
      |`./myscript1.sh
        ./myscript2.sh`
    ))
```

