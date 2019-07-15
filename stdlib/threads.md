---
nav: toc
---

# Multithreading

Operators and functions for working with threads \(**thread** type\) are described here.

* [resume\( thread th \)](threads.md#resume-thread-th)
* [sleep\( int duration \)](threads.md#sleep-int-duration)
* [suspend\( thread th \)](threads.md#suspend-thread-th)
* [terminate\( thread th \)](threads.md#terminate-thread-th)
* [wait\( thread th \)](threads.md#wait-thread-th)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| thread **=** thread |  | Assignment operator. |

## Functions

### resume\(thread th\)

The _resume_ function continues the work of the thread that was stopped by _suspend_ function.

### sleep\(int duration\)

The _sleep_ function pauses the current thread for at least the _duration_, in milliseconds.

### suspend\(thread th\)

The _suspend_ function suspends the _th_ thread. Use the _resume_ function to continue the thread.

### terminate\(thread th\)

The _terminate_ function terminates the thread. If the thread has already completed, the function does nothing.

### wait\(thread th\)

The _wait_ function waits for the _th_ thread to finish. If the thread has already finished, the function does nothing.

