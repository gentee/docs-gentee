# Multithreading

The Gentee language allows you to create multi-threaded scripts. In this case, part of the script can be performed in parallel, which reduces the time of its work. To execute some code in a separate thread, you must specify it in the **go** statement. The script will continue to perform the following constructions without waiting for the end of the code inside _go_, but immediately after the new thread is launched. The **go** statement returns the identifier of the created thread, which can be assigned to a variable of the **thread** type and then used in the multithreading functions. If the script has finished its work earlier than the child threads, then it will wait for all threads to finish working. If an error occurs in any of the threads while executing a multi-threaded script, all the threads are closed and the script returns this error.

```text
GoStmt = "go" [ "(" GoArgs ")" ] Block
GoArgs = identifier ":" Expression { "," identifier ":" Expression }
```

```text
func myThread {
  for i in 0..50 {
    Print(`x` )
    if i % 3 == 0 : sleep(5)
  }
}

run {
  thread th = go {
    for i in 0..100 {
      Print(` `, i )
      if i % 7 == 0 : sleep(5)
    }
  }
  suspend( th )
  go : myThread()
  resume(th)
  Print( `OK`)
  wait(th)
  Print( `END`)
}
```

You can pass any parameters in the **go** command. To do this, you need to specify the name of the parameter and its value separated by a colon. The type of the parameter is automatically determined by the passed value. If you pass structures or arrays, the parameter will be assigned a copy of the value.

```text
run str {
  str s = "ok"
  thread th1 = go (a: s + " test") : ctxPar #= a
  thread th2 = go (a: Max(1,23), b: Min(100,87)) {
     ctxSum #= a + b
  }
  wait(th2)
  wait(th1)
  return #ctxPar + #ctxSum
}
```

## 

