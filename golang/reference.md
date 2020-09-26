# Library Reference

The functions and structures for using the **Gentee** programming language in **Golang** projects are described here.

* [type Custom](reference.md#type-custom)
* [type EmbedItem](reference.md#type-embed-item)
* [type Settings](reference.md#type-settings)
* [Customize\(custom \*Custom\) error](reference.md#customize-custom-custom-error)
* [New\(\) \*Gentee](reference.md#new-gentee)
* [\(g \*Gentee\) Compile\(input, path string\) \(\*Exec, int, error\)](reference.md#g-gentee-compile-input-path-string-exec-int-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(interface{}, error\)](reference.md#g-gentee-compileandrun-filename-string-interface-error)
* [\(g \*Gentee\) CompileAndRun\(filename string\) \(\*Exec, int, error\)](reference.md#g-gentee-compilefile-filename-string-exec-int-error)
* [\(exec \*Exec\) Run\(settings Settings\) \(interface{}, error\)](reference.md#exec-exec-run-settings-settings-interface-error)
* [Gentee2GoType\(val interface{}, vtype... string\) interface{}](reference.md#gentee-2-gotype-val-interface-vtype-string-interface)
* [Go2GenteeType\(val interface{}, vtype... string\) \(interface{}, error\)](reference.md#go-2-genteetype-val-interface-vtype-string-interface-error)
* [Version\(\) string](reference.md#version-string)

## Types

### type Custom

The _Custom_ type is used for additional configuration of the compiler and virtual machine. It is passed when the **Customize** function is called.

* **Embedded** \[\]EmbedItem - an array of additional functions for the standard library.

### type EmbedItem


The _EmbedItem_ type describes the function to be embedded in the standard library. It is used in the **Custom** type.

* **Prototype** string - a description of the function in the Gentee language. For example, _myfunc\(str,int\) int_.
* **Object** interface{} - the corresponding golang function.

### type Settings

The _Settings_ type is used to specify additional parameters when starting the bytecode in the **Run** method.

* **CmdLine** \[\]string -  an array of command line parameters.
* **Stdin** \*os.File - custom standard input.
* **Stdout** \*os.File - custom standard output.
* **Stderr** \*os.File - custom error output.
* **Input** \[\]byte - predefined standard input (stdin). Can be used, for example, in the function [ReadString](/stdlib/console.md#readstring-string-text-str).
* **Cycle** uint64 - maximum number of iterations in the loop. By default, it is 1600000000.
* **Depth** uint32 - maximum nesting of executable blocks. Limits the recursion depth. By default, it is equal to 1000.
* **SysChan** chan int - the channel for sending *SysSuspend* (1), *SysResume* (2), *SysTerminate* (3) commands. It allows you to control the script execution from the outside.
  * *SysSuspend* - suspend the script execution and all its threads.
  * *SysResume* - resume the script execution and all its threads.
  * *SysTerminate* - terminate the script and all its threads.
* **IsPlayground** bool - assign *true* if you want to run the script in safe [playground](playground.md) mode.
* **Playground** Playground - configure the playground mode.
  * *Path* string - path to the temporary directory for writing and reading files. If it is not specified, the subdirectory in the temporary directory will be created.
  * *AllSizeLimit* int64 - total size of files. By default, it is 10 MB.
  * *FilesLimit* int - maximum number of files. By default, 100.
  * *SizeLimit* int64 - maximum file size. By default, 5 MB.

``` go
    settings.SysChan = make(chan int)
    go func() {
        _, err = exec.Run(settings)
    }()
    settings.SysChan <- gentee.SysTerminate
```

## Functions and methods

### Customize\(custom \*Custom\) error

The _Customize_ function is used for [additional settings of the compiler](customize.md) and virtual machine. It should be called before all the functions. The function returns the error value.

### New\(\) \*Gentee

The _New_ function creates a workspace for compiling source code.

### \(g \*Gentee\) Compile\(input, path string\) \(\*Exec, int, error\)

The _Compile_ function compiles the script passed to _input_. You can specify the path to the script in the _path_ parameter. The function returns a bytecode structure, module number and error value.

### \(g \*Gentee\) CompileAndRun\(filename string\) \(interface{}, error\)

The _CompileAndRun_ function compiles the script from the _filename_ file and executes it. The function returns the result of the script and the error value.

### \(g \*Gentee\) CompileFile\(filename string\) \(\*Exec, int, error\)

The _CompileFile_ function compiles the script from the _filename_ file. The function returns a bytecode structure, module number, and error value.

### \(exec \*Exec\) Run\(settings Settings\) \(interface{}, error\)

The _Run_ function executes bytecode from the _exec_ structure. You can specify additional settings in the _settings_ parameter. The function returns the result of the script and the error value.

### Gentee2GoType\(val interface{}, vtype... string\) interface{}

The _Gentee2GoType_ function converts the Gentee variable to standard Go types. In the second parameter, you can specify the Gentee type of a variable. For example, _arr.bool_. In this case you will get an array of variables of _bool_ type instead of _int64_. You can use this function in your embedded functions.

Type correspondence

| Gentee type | Param type | Result type (vtype)
| :--- | :--- | :--- |
| int | int64 | int64
| bool | int64 | bool ("bool")
| char | int64 | rune ("rune")
| float | float64 | float64
| str | string | string
| arr | *core.Array | []interface{}
| buf | *core.Buffer | []byte
| map | *core.Map | map[string]interface{}
| set | *core.Set | []byte
| struct type | *core.Struct | map[string]interface{}
| obj | *core.Obj | interface{}

```go
func cnv1(in *core.Map) (*core.Map, error) {
  my := gentee.Gentee2GoType(in).(map[string]interface{})
  for key, a := range my {
    for i, v := range a.([]interface{}) {
      a.([]interface{})[i] = v.(int64) + 1
    }
    delete(my, key)
    my[key+`2`] = a
  }
  ret, err := gentee.Go2GenteeType(my)
  return ret.(*core.Map), err
}
```

### Go2GenteeType\(val interface{}, vtype... string\) \(interface{}, error\)

The _Go2GenteeType_ function converts a value of the standard Go type to a value of Gentee type. In the second parameter you can specify the Gentee type of the variable. For example, _set_ if you want to convert _[]byte_ to *core.Set. You can use this function in your embedded functions.

Type correspondence

| Gentee type | Param type | Result type (vtype)
| :--- | :--- | :--- |
| int | all int & uint | int64
| bool | bool | int64
| char | rune | int64
| float | float64 | float64
| str | string | string
| arr | []interface{} | *core.Array
| buf | []byte | *core.Buffer
| set | []byte | *core.Set ("set")
| map | map[string]interface{} | *core.Map
| obj | interface{} | *core.Obj ("obj")

```go
func cnv5(in *core.Set) (*core.Set, error) {
  my := gentee.Gentee2GoType(in).([]byte)
  for i, b := range my {
    if i > 10 {
      break
    }
    if b == 0 {
      my[i] = 1
    } else {
      my[i] = b - 1
    }
  }
  ret, err := gentee.Go2GenteeType(my, `set`)
  return ret.(*core.Set), err
}
```

### Version\(\) string

The _Version_ function returns the current version number of the language.
