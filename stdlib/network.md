# Network

The functions for network/internet operations are described here.

* [Download\( str url, str filename \) int](network.md#download-str-url-str-filename-int)
* [HTTPGet\( str url \) buf](network.md#httpget-str-url-buf)
* [HTTPPage\( str url \) str](network.md#httppage-str-url-str)
* [HTTPRequest\( str url, str method, map.str params, map.str headers \) str](network.md#httprequest-str-url-str-method-map-str-params-map-str-headers-str)

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

### HTTPRequest\( str url, str method, map.str params, map.str headers \) str

The _HTTPRequest_ function sends an HTTP request to the specified URL and returns the response as a string. In the _method_ parameter you need to specify the calling method - **GET, POST, UPDATE, PUT, DELETE**. The function also allows you to specify parameters and request headers. They are described as associative arrays where parameter name or header name is specified as a key. By default, the parameters are passed as form data when *POST* is called. If you want to send them in JSON format, then specify *"Content-Type": "application/json; charset=UTF-8"* in the *headers* parameter.

``` go
    map empty
    Println(HTTPRequest(TESTURL, "GET", empty, empty))
    map params = { `name`: `Jong Doe`, `id`: `101` }
    Println(HTTPRequest(TESTURL, "GET", params, empty))
    Println(HTTPRequest(TESTURL, "POST", params, empty))
    map headjson = { `Content-Type`: `application/json; charset=UTF-8` }
    Println(HTTPRequest(TESTURL, "POST", params, headjson))
```
