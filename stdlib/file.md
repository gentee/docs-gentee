---
nav: toc
---

# Files

Functions for working with files and directories are described here.

* [AppendFile\( str filename, buf \| str data \)](file.md#appendfile-str-filename-buf-or-str-data)
* [ChDir\( str dirname \)](file.md#chdir-str-dirname)
* [ChMode\( str name, int mode \)](file.md#chmode-str-name-int-mode)
* [CopyFile\( str src, str dest \) int](file.md#copyfile-str-src-str-dest-int)
* [CreateDir\( str dirname \)](file.md#createdir-str-dirname)
* [CreateFile\( str name, bool trunc \)](file.md#createfile-str-name-bool-trunc)
* [ExistFile\( str name \) bool](file.md#existfile-str-name-bool)
* [FileInfo\( str name \) finfo](file.md#fileinfo-str-name-finfo)
* [FileMode\( str name \) int](file.md#filemode-str-name-int)
* [GetCurDir\(\) str](file.md#getcurdir-str)
* [IsEmptyDir\( str path \) bool](file.md#isemptydir-str-path-bool)
* [Md5File\( str filename \) str](file.md#md-5-file-str-filename-str)
* [obj\( finfo fi \) obj](file.md#obj-finfo-fi-obj)
* [ReadDir\( str dirname \) arr.finfo](file.md#readdir-str-dirname-arr-finfo)
* [ReadDir\( str dirname, int flags, str pattern \) arr.finfo](file.md#readdir-str-dirname-int-flags-str-pattern-arr-finfo)
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
* **int Mode** - file's mode and permission bits
* **time Time** - last modification time
* **bool IsDir** - true if it is a directory
* **str Dir** - directory where the file is located. This field is only filled when calling the function [ReadDir(str, int, str)](file.md#readdir-str-dirname-int-flags-str-pattern-arr-finfo)

## Functions

### AppendFile\(str filename, buf\|str data\)

The _AppendFile_ function appends data of _buf_ variable or a string to a file named by _filename_. If the file does not exist, _AppendFile_ creates it with 0644 permissions.

### ChDir\(str dirname\)

The _ChDir_ function changes the current directory.

### ChMode\(str name, int mode\)

The _ChMode_ function changes the attributes of the file.

### CopyFile\(str src, str dest\) int

The _CopyFile_ function copies _src_ file to _dest_ file. If _dest_ file exists it is overwritten. The file attributes are preserved when copying. The function returns the number of copied bytes.

### CreateDir\(str dirname\)

The _CreateDir_ function creates a directory named _dirname_, along with any necessary parents. If _dirname_ is already a directory, _CreateDir_ does nothing.

### CreateFile\(str name, bool trunc\)

The _CreateFile_ function creates a file with the specified name. If the _trunc_ parameter is _true_ and the file already exists, its size becomes 0.

### ExistFile\(str name\) bool

The _ExistFile_ function returns *true* if the specified file or directory exists. Otherwise, it returns *false*.

### FileInfo\(str name\) finfo

The _FileInfo_ function gets information about the named file and returns _finfo_ structure.

### FileMode\(str name\) int

The _FileMode_ function returns the file attributes.

### GetCurDir\(\) str

The _GetCurDir_ function returns the current directory.

### IsEmptyDir\(str path\) bool

The _IsEmptyDir_ function returns _true_ if the specified directory is empty. Otherwise, it returns _false_.

### Md5File\(str filename\) str

The _Md5File_ function returns the MD5 hash of the specified file as a hex string.

### obj\(finfo fi\) obj

The _obj_ function converts a variable of finfo type into an object. The resulting object has fields: *name, size, mode, time, isdir, dir*.

### ReadDir\(str dirname\) arr.finfo

The _ReadDir_ function reads the directory named by dirname and returns a list of directories and files entries.

### ReadDir\(str dirname, int flags, str pattern\) arr.finfo

The _ReadDir_ function reads the *dirname* directory with the specified name and returns the list of its subdirectories and files according to the specified parameters. The *flags* parameter can be a combination of the following flags:

* **RECURSIVE** - In this case there will be a recursive search for all subdirectories.
* **ONLYFILES** - The returned array will contain only files.
* **REGEXP** - The *pattern* parameter contains a regular expression for matching file names.

The *pattern* parameter can contain a wildcard for files or a regular expression. In this case, the files and directories that match the specified pattern will be returned. The wildcard can contain the following characters:

* '\*' - matches any sequence of non-separator characters
* '?' - matches any single non-separator character

``` go
for item in ReadDir(ftemp, RECURSIVE, `*fold*`) {
    ret += item.Name
}
for item in ReadDir(ftemp, RECURSIVE | ONLYFILES | REGEXP, `.*\.pdf`) {
    ret += item.Name
}
```

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

