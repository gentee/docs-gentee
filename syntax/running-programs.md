# Running programs

The language has a special command **$** to run applications and operating system commands with the specified parameters. The script takes the entire line up to the newline character and execute it. There must be a space between the **$** and the command line. If this command is used in an expression, it captures the standard output and returns it as a string. Otherwise, the standard output will be visible in the console. You can specify expressions with **%{Expression}** as in a backquoted string. If any parameter contains a space, enclose that parameter in any quotes - _"a b", 'c d', \`e f\`_. If the executable application or command terminates with an error code other than zero, the script will also stop working and return an error.

```text
Command = "$ " { unicode_linechar | "%{" Expression "}" | "${" identifier "}" }
```

```text
run str {
   $ dir
   str name = $ echo "John Smith"
   return $ echo My name is %{name}
}
```

### Environment Variables

The Gentee language allows you to easily get environment variables and assign values to them. To do this, specify the **$** character before the variable name. In addition, you can substitute the environment variables with the **${ENV\_NAME}** construct in the **$** launch commands and back-quoted strings. This entry is shorter than _%{ $ENV\_NAME }_. Environment variables are always of string type, but you can assign them values of **str**, **int**, and **bool** types.

```text
EnvVariable = "$" identifier
```

```text
run str {
    $MYVAR = `Go path: ${GOPATH}` + $GOROOT
    return $ echo ${MYVAR}
}
```

