---
nav: toc
---

# Files

Functions for working with files and directories are described here.

* [AppendFile\( str filename, buf \| str data \)](file.md#appendfile-str-filename-buf-or-str-data)
* [ChDir\( str dirname \)](file.md#chdir-str-dirname)
* [CopyFile\( str src, str dest \) int](file.md#copyfile-str-src-str-dest-int)
* [CreateDir\( str dirname \)](file.md#createdir-str-dirname)
* [FileInfo\( str name \) finfo](file.md#fileinfo-str-name-finfo)
* [GetCurDir\(\) str](file.md#getcurdir-str)
* [Md5File\( str filename \) str](file.md#md-5-file-str-filename-str)
* [ReadDir\( str dirname \) arr.finfo](file.md#readdir-str-dirname-arr-finfo)
* [ReadFile\( str filename \) str](file.md#readfile-str-filename-str)
* [ReadFile\( str filename, buf out \) buf](file.md#readfile-str-filename-buf-out-buf)
* [ReadFile\( str filename, int offset, int length \) buf](file.md#readfile-str-filename-int-offset-int-length-buf)
* [Remove\( str name \)](file.md#remove-str-name)
* [RemoveDir\( str dirname \)](file.md#removedir-str-dirname)
* [Rename\( str oldpath, str newpath \)](file.md#rename-str-oldpath-str-newpath)
* [SetFileTime\( str name, time modtime \)](file.md#setfiletime-str-name-time-modtime)
* [Sha256File\( str filename \) str](file.md#sha-256-file-str-filename-str)
* [TempDir\(\) str](file.md#tempdir-str)
* [TempDir\( str path, str prefix \) str](file.md#tempdir-str-path-str-prefix-str)
* [WriteFile\( str filename, buf \| str data \)](file.md#writefile-str-filename-buf-or-str-data)

## Types

### finfo

The _finfo_ is used for getting information about a file and has the following fields:

* **str Name** - base name of the file
* **int Size** - length in bytes for regular files
* **int Mode** - file's mode and permission bits.
* **time Time** - last modification time
* **bool IsDir** - true if it is a directory

## Functions

### AppendFile\(str filename, buf\|str data\)

The _AppendFile_ function appends data of _buf_ variable or a string to a file named by _filename_. If the file does not exist, _AppendFile_ creates it with 0644 permissions.

### ChDir\(str dirname\)

The _ChDir_ function changes the current directory.

### CopyFile\(str src, str dest\) int

The _CopyFile_ function copies _src_ file to _dest_ file. If _dest_ file exists it is overwritten. The function returns the number of copied bytes.

### CreateDir\(str dirname\)

The _CreateDir_ function creates a directory named _dirname_, along with any necessary parents. If _dirname_ is already a directory, _CreateDir_ does nothing.

### FileInfo\(str name\) finfo

The _FileInfo_ function gets information about the named file and returns _finfo_ structure.

### GetCurDir\(\) str

The _GetCurDir_ function returns the current directory.

### Md5File\(str filename\) str

The _Md5File_ function returns the MD5 hash of the specified file as a hex string.

### ReadDir\(str dirname\) arr.finfo

The _ReadDir_ function reads the directory named by dirname and returns a list of directories and files entries.

### ReadFile\(str filename\) str

The _ReadFile_ function reads the specified file and returns the contents as a string.

### ReadFile\(str filename, buf out\) buf

The _ReadFile_ function reads the file named by _filename_ to the _buf_ variable _out_ and returns it.

### ReadFile\(str filename, int offset, int length\) buf

The _ReadFile_ function reads data from the _filename_ file starting at offset _offset_ and length _length_. If _offset_ is less than zero, then the offset is counted from the end to the beginning of the file.

### Remove\(str name\)

The _Remove_ function removes a file or an empty directory.

### RemoveDir\(str dirname\)

The _RemoveDir_ function removes _dirname_ directory and any children it contains.

### Rename\(str oldpath, str newpath\)

The _Rename_ function renames \(moves\) _oldpath_ to _newpath_. If _newpath_ already exists and is not a directory, _Rename_ replaces it.

### SetFileTime\(str name, time modtime\)

The _SetFileTime_ function changes the modification time of the named file.

### Sha256File\(str filename\) str

The _Sha256File_ function returns the SHA256 hash of the specified file as a hex string.

### TempDir\(\) str

The _TempDir_ function returns the default temporary directory.

### TempDir\(str path, str prefix\) str

The _TempDir_ function creates a new temporary directory in the directory _path_ with a name beginning with _prefix_ and returns the path of the new directory. If _path_ is the empty string, _TempDir_ uses the default temporary directory.

### WriteFile\(str filename, buf\|str data\)

The _WriteFile_ function writes data of _buf_ variable or a string to a file named by _filename_. If the file does not exist, _WriteFile_ creates it with 0777 permissions, otherwise the file is truncated before writing.

