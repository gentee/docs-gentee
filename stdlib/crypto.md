# Cryptography

The cryptographic functions are described below.

* [AESDecrypt\( str key, buf data \) buf](crypto.md#aesdecrypt-str-key-buf-data-buf)
* [AESEncrypt\( str key, buf data \) buf](crypto.md#aesencrypt-str-key-buf-data-buf)
* [Md5\( buf \| str data \) buf](crypto.md#md-5-buf-or-str-data-buf)
* [RandomBuf\( int size \) buf](crypto.md#randombuf-int-size-buf)
* [Sha256\( buf \| str data \) buf](crypto.md#sha-256-buf-or-str-data-buf)

## Functions

### AESDecrypt\( str key, buf data \) buf

The _AESDecrypt_ function decrypts the content of the *buf* variable using the *key* encryption key. The encrypted data must be obtained using the *AESEncrypt* function. The function returns a variable of the *buf* type with decrypted data.

``` go
buf encrypted = AESDecrypt(`my password`, encrypted)
```

### AESEncrypt\( str key, buf data \) buf

The _AESEncrypt_ function encrypts the content of a *buf* variable using the AES-256 algorithm. The *key* parameter is an encryption key. The function returns a variable of *buf* type with encrypted data. Use the *AESDecrypt* function to decrypt the data.

``` go
buf crypted = AESEncrypt(`my password`, buf(`Test message`))
```

### Md5\(buf\|str data\) buf

The _Md5_ function returns MD5 hash of the _buf_ or _str_ type variable. 

### RandomBuf\(int size\) buf

The _RandomBuf_ function returns a variable of the *buf* type that contains a sequence of random bytes of the specified size.

### Sha256\(buf\|str data\) buf

The _Sha256_ function returns SHA5 hash of the _buf_ or _str_ type variable. 
