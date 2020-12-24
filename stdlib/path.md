# Path

The functions for manipulating filename paths are described here.

* [AbsPath\( str path \) str](path.md#abspath-str-path-str)
* [BaseName\( str path \) str](path.md#basename-str-path-str)
* [Dir\( str path \) str](path.md#dir-str-path-str)
* [Ext\( str path \) str](path.md#ext-str-path-str)
* [JoinPath\( str path... \) str](path.md#joinpath-str-path-str)
* [MatchPath\( str pattern, str path \) bool](path.md#matchpath-str-pattern-str-path-bool)
* [Path\( finfo fi \) str](path.md#path-finfo-fi-str)

## Functions

### AbsPath\(str path\) str

The _AbsPath_ function returns an absolute representation of path.

### BaseName\(str path\) str

The _BaseName_ function returns the last element of path. Trailing path separators are removed before extracting the last element. If the path is empty, the function returns ".".

### Dir\(str path\) str

The _Dir_ function returns all but the last element of path, typically the path's directory.

### Ext\(str path\) str

The _Ext_ function returns the file name extension. The result extension is without a dot.

### JoinPath\(str path...\) str

The _JoinPath_ function joins any number of path elements into a single path, adding a separator if necessary.

### MatchPath\(str pattern, str path\) bool

The _MatchPath_ function checks if the given name matches the specified pattern. The function checks the pattern completely for the specified path, not for the substring. You can use a regular expression as a pattern. To do this, add a */* at the beginning and end.

* '\*' - matches any sequence of non-separator characters
* '?' - matches any single non-separator character

```text
MatchPath(`*.txt`, `myfile.txt`)       // true
MatchPath(`?a?.pdf`, `1ab.pdf`)        // true
MatchPath(`/home/ak/my.pdf`, `*.pdf`)         // false
MatchPath(`/home/ak/my.pdf`, `/home/*/my.*`)  // true
MatchPath(`/home/ak/my.pdf`, `/home/*/my.*`) // true
MatchPath(`/user/`, `/home/user/myfile`) // true
```

### Path\(finfo fi\) str

The _Path_ function concatenates the *Name* and *Dir* fields of the *finfo* variable and returns the resulting path.
