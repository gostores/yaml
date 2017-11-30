## Installation and usage

To install, run:

```
$ go get github.com/gostores/yamlstructure
```

And import using:

```
import "github.com/gostores/yamlstructure"
```

Usage is very similar to the JSON library:

```go
package main

import (
	"fmt"

	"github.com/gostores/yamlstructure"
)

type Person struct {
	Name string `json:"name"` // Affects YAML field names too.
	Age  int    `json:"age"`
}

func main() {
	// Marshal a Person struct to YAML.
	p := Person{"John", 30}
	y, err := yamlstructure.Marshal(p)
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	fmt.Println(string(y))
	/* Output:
	age: 30
	name: John
	*/

	// Unmarshal the YAML back into a Person struct.
	var p2 Person
	err = yamlstructure.Unmarshal(y, &p2)
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	fmt.Println(p2)
	/* Output:
	{John 30}
	*/
}
```

`yamlstructure.YAMLToJSON` and `yamlstructure.JSONToYAML` methods are also available:

```go
package main

import (
	"fmt"

	"github.com/gostores/yamlstructure"
)

func main() {
	j := []byte(`{"name": "John", "age": 30}`)
	y, err := yamlstructure.JSONToYAML(j)
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	fmt.Println(string(y))
	/* Output:
	name: John
	age: 30
	*/
	j2, err := yamlstructure.YAMLToJSON(y)
	if err != nil {
		fmt.Printf("err: %v\n", err)
		return
	}
	fmt.Println(string(j2))
	/* Output:
	{"age":30,"name":"John"}
	*/
}
```
