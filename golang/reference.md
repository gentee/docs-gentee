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
* **Input** \[\]byte - predefined standard input (stdin). Can be used, for example, in the function [ReadString](/stdlib/console.md#readstring-string-text-str).
* **Cycle** uint64 - maximum number of iterations in the loop. By default, it is 1600000000.
* **Depth** uint32 - maximum nesting of executable blocks. Limits the recursion depth. By default, it is equal to 1000.

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

### Version\(\) string

The _Version_ function returns the current version number of the language.

