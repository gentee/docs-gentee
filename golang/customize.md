# Advanced features

## How to add your functions to the standard library

When using **Gentee** in other projects, it may be necessary to expand the standard library. The **Customize** function allows you to add any number of go-functions to the standard library and use them in scripts. It should be noted that in this case the scripts will not be compiled by the original compiler, since there will be no added functions there. The **Customize** function must be called before calling other functions from the gentee package.

To expand the standard library, you should specify an array of functions in the parameter of the [*Custom*](reference.md#type-custom) type. Each function is described by the structure [*EmbedItem*](reference.md#type-embed-item), in which a prototype in the Gentee language and the function itself are specified. The function may return a value of the *error* type and have a variable number of parameters.

### Type correspondence

Parameters and return value of go-functions must have types in accordance with this table. When using *core* types, you must import *github.com/gentee/gentee/core*.

| Gentee type | Golang type |
| :--- | :--- | :--- |
| int | int64 |
| bool | int64 |
| char | int64 |
| thread | int64 |
| float | float64 |
| str | string |
| arr | *core.Array |
| buf | *core.Buffer |
| map | *core.Map |
| set | *core.Set |
| struct type | *core.Struct |

```go
func sum(x, y int64) int64 {
	return x + 2*y
}

func varInt(init int64, pars ...int64) int64 {
	for _, i := range pars {
		init += i
	}
	return init
}

func shortLen(s string) (int64, error) {
	if len(s) < 10 {
		return len(s), nil
	}
	return 0, fmt.Errorf("string %s is too long", s)
}

func main() {
    var customLib = []gentee.EmbedItem{
        {Prototype: `sum(int,int) int`, Object: sum},
        {Prototype: `InitSum(int) int`, Object: varInt},
        {Prototype: `ShortLen(str) int`, Object: shortLen},
    }
    err := gentee.Customize(&gentee.Custom{
		Embedded: customLib,
	})
	if err != nil {
		log.Fatal(err)
    }
    workspace := gentee.New()
    exec, _, err := workspace.Compile(`run {
    Println("Sum = %{sum(10, 6)}")
    Println("InitSum = " + InitSum(4, 67, 4, 22))
    ShortLen("this string is too long")
}`, ``)
    ...
}
```