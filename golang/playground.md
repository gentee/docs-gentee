
# The Gentee playground

If you want to allow third parties to run Gentee scripts on your computer, use the *Playground* mode when running the scripts. This mode is convenient to run scripts for demonstration or educational purposes and protects the data on your computer from accidental or intentional damage. To enable this mode, specify the *Playground* field as *true* in the *Settings* structure when launching a script using the *Run* function. In addition, it is recommended to reduce the *Cycle* and *Depth* parameters to set limits on resources consumed.

Scripts working in the *Playground* mode have the following restrictions:

* **Processes**. Disabled launches of any processes, including opening files in the corresponding applications. In other words, the functions *Open, OpenWith, Run, Start* will not work. The **$** command will not work too.
* **File system**. The files could be written and read only in the directory, which is specified in the Playground settings. If it is not specified, the subdirectory is created in the temporary directory. This subdirectory becomes current at script start. In addition, there are restrictions on:
    * the total number of files (by default, 100).
    * total file size (by default, 10 MB).
    * maximum file size (by default, 5 MB).
* **Network**. *HTTPRequest* function is disabled. Calling the *Download, HTTPGet, HTTPPage* functions virtually adds a file with the corresponding size to the playground directory. Thus, these functions are also restricted by the file system restrictions.

If an error occurs during the script operation due to *Playground* mode restrictions, the script will stop working. In this case, the error text will begin with **[Playground]**.

``` go
run {
    $ echo "ooops"
}
// ERROR: [2:5] [Playground] starting any processes is disabled
run {
    AppendFile(".../out.txt", "this is a test message")
}
// ERROR: [2:5] [Playground] access denied [.../out.txt]
run {
    for i in 1...110 {
        CreateFile(`%{i}.txt`, false)
    }
}
// ERROR: [3:9] [Playground] file limit reached [100]
```
