---
nav: toc
---

# Multithreading

Operators and functions for working with threads \(**thread** type\) are described here.

* [Lock\(\)](threads.md#lock)
* [resume\( thread th \)](threads.md#resume-thread-th)
* [sleep\( int duration \)](threads.md#sleep-int-duration)
* [suspend\( thread th \)](threads.md#suspend-thread-th)
* [terminate\( thread th \)](threads.md#terminate-thread-th)
* [Unlock\(\)](threads.md#unlock)
* [wait\( thread th \)](threads.md#wait-thread-th)
* [WaitAll\(\)](threads.md#waitall)
* [WaitDone\(\)](threads.md#waitdone)
* [WaitGroup\( int count \)](threads.md#waitgroup-int-count)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| thread **=** thread |  | Assignment operator. |

## Functions

### Lock\(\)

The _Lock_ function blocks access to the global resource (mutex). If it is already occupied by another thread, then the current thread is waiting for it to be released. The mutex must be freed using the _Unlock_ function.

### resume\(thread th\)

The _resume_ function continues the work of the thread that was stopped by _suspend_ function.

### sleep\(int duration\)

The _sleep_ function pauses the current thread for at least the _duration_, in milliseconds.

### suspend\(thread th\)

The _suspend_ function suspends the _th_ thread. Use the _resume_ function to continue the thread.

### terminate\(thread th\)

The _terminate_ function terminates the thread. If the thread has already completed, the function does nothing.

### Unlock\(\)

The _Unlock_ function releases access to a global resource (mutex).

### wait\(thread th\)

The _wait_ function waits for the _th_ thread to finish. If the thread has already finished, the function does nothing.

### WaitAll\(\)

The _WaitAll_ function waits when the _WaitGroup_ counter becomes zero.

```go
run {
  int count = 3
  WaitGroup(count)
  for i in 1..count {
    go {
      // ...
      WaitDone()
    }
  }
  WaitAll()
}
```

### WaitDone\(\)

The _WaitDone_ function decreases the counter _WaitGroup_ by one.

### WaitGroup\(int count\)

The _WaitGroup_ function creates a _WaitGroup_ counter for the threads that should end with a calling the _WaitDone_ function. _count_ - the initial value of the counter.
