---
nav: toc
---

# Map

Operators and functions for working with map arrays \(**map** type\) are described here. **map.typename** means that you can specify any type name but in the case of the binary operator this type must be the same in both maps.

## Operators

| Operator | Result | Description |
| :--- | :--- | :--- |
| **\*** map.typename | int | Returns the number of elements in the map. |
| map.typename **=** map.typename | map.typename | Assignment operator. |
| map.typename **&=** map.typename | map.typename | Creates a clone of the map. The new variable will work with the same data set. |
| map.typename **\[** str **\]** | typename | Sets/gets a map value by key. |

