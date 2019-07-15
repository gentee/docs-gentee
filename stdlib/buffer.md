---
nav: toc
---

# Buffer

Operators and functions for working with an array of bytes \(**buf** type\) are described here.

* [buf\( str s \) buf](buffer.md#buf-str-s-buf)
* [str\( buf b \) str](buffer.md#str-buf-b-str)
* [Del\( buf b, int off, int length \) buf](buffer.md#del-buf-b-int-off-int-length-buf)
* [Hex\( buf b \) str](buffer.md#hex-buf-b-str)
* [Insert\( buf b, int off, buf src\) buf](buffer.md#insert-buf-b-int-off-buf-src-buf)
* [UnHex\( str s \) buf](buffer.md#unhex-str-s-buf)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** buf | int | Returns the number of bytes in the array. |
| buf **+** buf | buf | Merges two buffers. |
| buf **=** buf | buf | Assignment operator. |
| buf **&=** buf | buf | Create a clone of the buffer. The new variable will work with the same data set. |
| buf **+=** buf | buf | Appends a buffer to a buffer variable. |
| buf **+=** int | buf | Appends one byte to the buffer. The number must be less than 256. |
| buf **+=** str | buf | Appends a string to the buffer. |
| buf **+=** char | buf | Appends a character to the buffer. |
| buf **\[** int **\]** | int | Sets/gets a byte by index. |

## Functions

### buf\(str s\) buf

The _buf_ function converts a string to a _buf_ value and returns it.

### str\(buf b\) str

The _str_ function converts a _buf_ value to a string and returns it.

### Del\(buf b, int off, int length\) buf

The _Del_ function removes part of the data from the byte array. _off_ is the offset of the data to be deleted, _length_ is the number of bytes to be deleted. If _length_ is less than zero, then the data will be deleted to the left of the specified offset. The function returns the _b_ variable in which the deletion occurred.

### Hex\(buf b\) str

The _Hex_ function encodes a _buf_ value to a hexadecimal string and returns it.

### Insert\(buf b, int off, buf src\) buf

The _Insert_ function inserts an array of bytes _src_ into the array _b_. _off_ is the offset where the specified byte array will be inserted. The function returns the variable _b_.

### UnHex\(str s\) buf

The _UnHex_ function returns the _buf_ value represented by the hexadecimal string _s_. The input string must contain only hexadecimal characters.

