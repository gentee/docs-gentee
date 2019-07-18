# Network

The functions for network/internet operations are described here.

* [Download\( str url, str filename \) int](network.md#download-str-url-str-filename-int)
* [HTTPGet\( str url \) buf](network.md#httpget-str-url-buf)
* [HTTPPage\( str url \) str](network.md#httppage-str-url-str)

## HTTP functions

### Download\( str url, str filename \) int

The _Download_ function downloads the file from the specified URL and saves it with the specified filename. The function returns the size of the downloaded file.

```go
    str ftemp = TempDir() + `/readme.html`
    int size = Download("https://github.com/gentee/gentee", ftemp)
```

### HTTPGet\( str url \) buf

The _HTTPGet_ function sends a GET request to the specified URL and returns a response as a _buf_ variable. The function can be used to download small files without saving them to disk.

### HTTPPage\( str url \) str

The _HTTPPage_ function sends a GET request to the specified URL and returns a string response.
