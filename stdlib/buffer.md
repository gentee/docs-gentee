---
nav: toc
---

# Buffer

Operators and functions for working with an array of bytes \(**buf** type\) are described here.

* [bool\( buf b \) bool](buffer.md#bool-buf-b-bool)
* [buf\( str s \) buf](buffer.md#buf-str-s-buf)
* [str\( buf b \) str](buffer.md#str-buf-b-str)
* [Base64\( buf b \) str](buffer.md#base-64-buf-b-str)
* [DecodeInt\( buf b, int offset \) int](buffer.md#decodeint-buf-b-int-offset-int)
* [Del\( buf b, int off, int length \) buf](buffer.md#del-buf-b-int-off-int-length-buf)
* [EncodeInt\( buf b, int i \) buf](buffer.md#encodeint-buf-b-int-i-buf)
* [Hex\( buf b \) str](buffer.md#hex-buf-b-str)
* [Insert\( buf b, int off, buf src\) buf](buffer.md#insert-buf-b-int-off-buf-src-buf)
* [SetLen\( buf b, int size \) buf](buffer.md#setlen-buf-b-int-size-buf)
* [Subbuf\( buf b, int off, int length \) buf](buffer.md#subbuf-buf-b-int-off-int-length-buf)
* [UnBase64\( str s \) buf](buffer.md#unbase-64-str-s-buf)
* [UnHex\( str s \) buf](buffer.md#unhex-str-s-buf)
* [Write\( buf b, int off, buf src \) buf](buffer.md#write-buf-b-int-off-buf-src-buf)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** buf | int | Returns the number of bytes in the array. |
| buf **?** | bool | Calls *bool(buf)*. |
| buf **+** buf | buf | Merges two buffers. |
| buf **=** buf | buf | Assignment operator. |
| buf **&=** buf | buf | Create a clone of the buffer. The new variable will work with the same data set. |
| buf **+=** buf | buf | Appends a buffer to a buffer variable. |
| buf **+=** int | buf | Appends one byte to the buffer. The number must be less than 256. |
| buf **+=** str | buf | Appends a string to the buffer. |
| buf **+=** char | buf | Appends a character to the buffer. |
| buf **\[** int **\]** | int | Sets/gets a byte by index. |

## Functions

### bool\(buf b\) bool

The _bool_ function returns _false_ if the buffer is empty, otherwise, it returns _true_.

### buf\(str s\) buf

The _buf_ function converts a string to a _buf_ value and returns it.

### str\(buf b\) str

The _str_ function converts a _buf_ value to a string and returns it.

### Base64\(buf b\) str

The _Base64_ function converts a value of the _buf_ type into a string in __base64__ encoding and returns it.

### DecodeInt\(buf b, int offset\) int

The _DecodeInt_ function gets an integer from a parameter of _buf_ type.  _offset_ is the offset in the buffer at which to read the number. The function reads 8 bytes and returns them as an integer.

### Del\(buf b, int off, int length\) buf

The _Del_ function removes part of the data from the byte array. _off_ is the offset of the data to be deleted, _length_ is the number of bytes to be deleted. If _length_ is less than zero, then the data will be deleted to the left of the specified offset. The function returns the _b_ variable in which the deletion occurred.

### EncodeInt\(buf b, int i\) buf

The _EncodeInt_ function appends an integer number to a specified variable of _buf_ type. Since the *int* value occupies 8 bytes, 8 bytes are appended to the buffer regardless of the _i_ parameter value. The function returns the *b* parameter.

### Hex\(buf b\) str

The _Hex_ function encodes a _buf_ value to a hexadecimal string and returns it.

### Insert\(buf b, int off, buf src\) buf

The _Insert_ function inserts an array of bytes _src_ into the array _b_. _off_ is the offset where the specified byte array will be inserted. The function returns the variable _b_.

### SetLen\(buf b, int size\) buf

The _SetLen_ function sets the size of the buffer. If _size_ is less than the size of the buffer, then it will be truncated. Otherwise, the buffer will be padded with zeros to the specified size.

### Subbuf\(buf b, int off, int length\) buf

The _Subbuf_ function returns a new buffer that contains the chunk of the _b_ buffer with the specified offset and length.

### UnBase64\(str s\) buf

The _UnBase64_ function converts a string in __base64__ encoding into a value of the _buf_ type and returns it.

### UnHex\(str s\) buf

The _UnHex_ function returns the _buf_ value represented by the hexadecimal string _s_. The input string must contain only hexadecimal characters.

### Write\(buf b, int off, buf src\) buf

The _Write_ function writes the byte array of the _src_ variable into the _b_ variable starting from the specified offset. The data is written over existing values. The function returns variable _b_.
