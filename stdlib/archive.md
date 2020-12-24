# Archiving

The functions for working with **zip** and **tar.gz** archives are described here.

* [ArchiveName\( finfo fi, str root \) str](archive.md#archivename-finfo-fi-str-root-str)
* [CloseTarGz\( handle h \)](archive.md#closetargz-handle-h)
* [CloseZip\( handle h \)](archive.md#closezip-handle-h)
* [CreateTarGz\( str name \) handle](archive.md#createtargz-str-name-handle)
* [CreateZip\( str name \) handle](archive.md#createzip-str-name-handle)
* [CompressFile\( handle h, str fname, str packname \)](archive.md#compressfile-handle-h-str-fname-str-packname)
* [ReadTarGz\( str name \) arr.finfo](archive.md#readtargz-str-name-arr-finfo)
* [ReadZip\( str name \) arr.finfo](archive.md#readzip-str-name-arr-finfo)
* [TarGz\( str name, str path \)](archive.md#targz-str-name-str-path)
* [UnpackTarGz\( str name, str path \)](archive.md#unpacktargz-str-name-str-path)
* [UnpackTarGz\( str name, str path, arr pattern, arr ignore \)](archive.md#unpacktargz-str-name-str-path-arr-pattern-arr-ignore)
* [UnpackZip\( str name, str path \)](archive.md#unpackzip-str-name-str-path)
* [UnpackZip\( str name, str path, arr pattern, arr ignore \)](archive.md#unpackzip-str-name-str-path-arr-pattern-arr-ignore)
* [Zip\( str name, str path \)](archive.md#zip-str-name-str-path)

## Functions

### ArchiveName\(finfo fi, str root\) str

The _ArchiveName_ function concatenates the *Name* and *Dir* fields in a variable of *finfo* type and returns the file path for the archive relative to the root path *root*.

### CloseTarGz\(handle h\)

The _CloseTarGz_ function finishes creating the *.tar.gz* archive. The _h_ parameter is the identifier that was returned by the **CreateTarGz** function.

### CloseZip\(handle h\)

The _CloseZip_ function finishes creating the *.zip* archive. The _h_ parameter is the identifier that was returned by the **CreateZip** function.

### CreateTarGz\(str name\) handle

The _CreateTarGz_ function starts creating a **.tar.gz** archive with the specified name. You can add files to this archive with the **CompressFile** function. The function returns an identifier, which you will need to close with the _CloseTarGz_ function.

### CreateZip\(str name\) handle

The _CreateZip_ function starts creating a **.tar.gz** archive with the specified name. You can add files to this archive with the **CompressFile** function. The function returns an identifier, which you will need to close with the _CloseZip_ function.

### CompressFile\(handle h, str fname, str packname\)

The _CompressFile_ function adds the specified _fname_ file to the created archive. The _packname_ parameter contains the relative path and file name  to be saved in the archive. Use **/** symbol as a separator. The archive must be previously created using the **CreateZip** or **CreateTarGz** functions.

``` go
    handle zip = CreateZip(`my.zip`)
    CompressFile(zip, `../data/my.txt`, `my.txt`)
    CompressFile(zip, `/home/user/folder/copy.txt`, `folder/copy.txt`)
    CloseZip(zip)
```

### ReadTarGz\(str name\) arr.finfo

The _ReadTarGz_ function returns the list of files in the specified **tar.gz** archive. The *Name* field contains the file name together with the relative path.

``` go
   arr.finfo list = ReadTarGz(`my.tar.gz`)
   for fi in list : Println( "\{fi.Name} \{fi.Size}")
```

### ReadZip\(str name\) arr.finfo

The _ReadZip_ function returns the list of files in the specified **.zip** archive. The *Name* field contains the file name together with the relative path.

### TarGz\(str name, str path\)

The _TarGz_ function packs the file or the contents of the _path_ directory into a **.tar.gz** archive named _name_.

``` go
   TarGz("/home/user/out/my.tar.gz", `/home/user/docs`)
```

### UnpackTarGz\(str name, str path\)

The _UnpackTarGz_ function unpacks a **.tar.gz** archive named _name_ into the _path_ directory.

``` go
   UnpackTarGz("/home/user/out/my.tar.gz", `/home/user/olddocs`)
```

### UnpackTarGz\(str name, str path, arr pattern, arr ignore\)

The _UnpackTarGz_ function selectively unpacks a **.tar.gz** archive named _name_ into the _path_ directory. The _pattern_ array contains file patterns to be unpacked. The _ignore_ array contains file patterns to skip. The _pattern_ and _ignore_ parameters can be empty arrays. If the pattern begins and ends with **/**, then it is treated as a regular expression.

``` go
   arr empty
   arr doc = {`*.docx`, `/.txt$/`}
   UnpackTarGz("/home/user/out/my.tar.gz", `/home/user/tmp`, doc, empty )
```

### UnpackZip\(str name, str path\)

The _UnpackZip_ function unpacks a **.zip** archive named _name_ into the _path_ directory.

``` go
   UnpackZip("/home/user/out/my.zip", `/home/user/olddocs`)
```

### UnpackZip\(str name, str path, arr pattern, arr ignore\)

The _UnpackZip_ function selectively unpacks a **.tar.gz** archive named _name_ into the _path_ directory. The _pattern_ array contains file patterns to be unpacked. The _ignore_ array contains file patterns to skip. The _pattern_ and _ignore_ parameters can be empty arrays. If the pattern begins and ends with **/**, then it is treated as a regular expression.

``` go
   arr empty
   arr skip = {`/temp.pdf/`, `/.txt$/`}
   UnpackZip("/home/user/out/my.tar.gz", `/home/user/tmp`, empty, skip )
```

### Zip\(str name, str path\)

The _Zip_ function packs the file or the contents of the _path_ directory into a **.zip** archive named _name_.

``` go
   Zip("/home/user/out/mydoc.zip", `/home/user/docs/important.docx`)
```
