#algo2

```go
func invertir[T any] (elems []T) []T {
	total := len(elems)
	res := make([]T, total)
	for i := range elems {
		res[total-i-1] = elems[i]	
	}
	
	return res
}
```

- Type parameter: estamos indicando el nombre del tipo y el **Type constraint** me dice qué tipos pueden usarse con esta función
- En la variable `res` se usa el tiop definido en la constraint para recibir, instanciar y devolver lo que necesitemos
```go
import "<modulo>/utils"

func main() {
	numeros := []int{1,2,3,4,5}
	letritas := []string("a", "b", "c", "d")
	
	intsInvertidos := utils.invertir[int](numeros)
	letrasInvertidas := utils.invertir[string](letritas)
}
```

## Structs
```go
type ArregloDinamico[T any] struct {
	arregloInterno []T
}

func (a *ArregloDinamico) Append(elem T) {
	a.arregloInterno = append(a.arregloInterno, elem)
}

func main() {
	arreglo := ArregloDinamico[int]()
	arreglo.Append(4)
}
```

## Custom constraints
```go
type AB interface {
	*A | *B
	algo() bool
}

func funcion[T AB](x T) bool {
	return x.algo()
}

func main() {
	a := &A{}
	b := &B{}
	fmt.Println(funcion(a))
	fmt.Println(funcion(b))
}
```