---
description: Gentee programming language documentation
---

# Gentee script programming language

Gentee is a strongly typed procedural language. First of all, it is designed to write scripts to automate repetitive actions and processes on the computer. The Gentee language has a simple syntax and it is easy to learn and maintain.

**GitHub repository:** [**https://github.com/gentee/gentee**](https://github.com/gentee/gentee)  
**Download for Linux, macOS, Windows:** [**https://github.com/gentee/gentee/releases**](https://github.com/gentee/gentee/releases)  
Documentation GitHub repository: [https://github.com/gentee/docs-gentee](https://github.com/gentee/docs-gentee)  
Development language: Go

```go 
run : ||"Hello, world!\r\n"
```
```go 
run : $ echo "Hello, world!"
```
```go 
run {
    str name = ReadString(`Enter your name: `)
    Println(`Hello, %{ ?(*name>0, name, `world`) }!` )
}
```
## Documentation

* [Gentee Programming language \(English\)](https://docs.gentee.org)
* [Язык программирования Gentee \(Russian\)](https://ru.gentee.org)
