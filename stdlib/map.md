# Map

Operators and functions for working with map arrays \(**map** type\) are described here. **map.typename** means that you can specify any type name but in the case of the binary operator this type must be the same in both maps.

* [bool\( map.typename m \) bool](map.md#bool-map-typename-m-bool)
* [Del\( map.typename m, str key \) map.typename](map.md#del-map-typename-m-str-key-map-typename)
* [IsKey\( map.typename m, str key \) bool](map.md#iskey-map-typename-m-str-key-bool)
* [Key\( map.typename m, int index \) str](map.md#key-map-typename-m-int-index-str)

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** map.typename | int | Returns the number of elements in the map. |
| map.typename **?** | bool | Calls *bool(map.typename)*. |
| map.typename **=** map.typename | map.typename | Assignment operator. |
| map.typename **&=** map.typename | map.typename | Creates a clone of the map. The new variable will work with the same data set. |
| map.typename **\[** str **\]** | typename | Sets/gets a map value by key. |

## Functions

### bool\(map.typename m\) bool

The _bool_ function returns _false_ if the map is empty, otherwise, it returns _true_.

### Del\( map.typename m, str key \) map.typename

The _Del_ function deletes the specified key and its value from the _map_ array. The _m_ parameter is returned.

### IsKey\( map.typename m, str key \) bool

The _IsKey_ function returns _true_ if there is a value with the specified key in the _map_ and _false_, otherwise.

### Key\( map.typename m, int index \) str

The _Key_ function returns the item key by its index. For example, this function can be used in the *for* loop to get the item key.

``` go 
for val,i in mymap {
    Println("\(Key(mymap, i)):\(val)")
}
```