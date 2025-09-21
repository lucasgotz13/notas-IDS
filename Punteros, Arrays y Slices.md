#algo2
## Punteros

### Para que se usan?

- Referenciar indirectamente a variables locales
- Permitir que funciones puedan modificar variables externas.
- Es la manera de trabajar con memoria dinámica. El compilador decide qué punteros están en el heap y cuales están en el stack.

### Como usar a los punteros?

```go
import "fmt"

func pasaUnDia(valor *int) {
	*valor = *valor * 2
}

func main() {
	var dolar int = 10
	fmt.Printf("Ahora vale %d\n", dolar)
	pasaUnDia(&dolar)
	fmt.Printf("Ahora vale %d\n", dolar)
}
```

## Arrays

- Secuencia de elementos
- Se crean con tamaño fijo que no se puede modificar
- Los elementos se encuentran contiguos en memoria
- Las posiciones van de 0 a N-1 (siendo N el tamaño del array)

```go
var arreglo [4]int = [4]int{1,2,3,4}
fmt.Println(arreglo[0]) // 1
fmt.Println(arreglo[3]) // 4
arreglo[3] = 5
fmt.Println(arreglo) // [1 2 3 5]

var arreglo2 := [4]int{1,2,3}
fmt.Println(arreglo) // [1 2 3 0]
fmt.Println(len(arreglo)) // 4
```

```go
arreglo := [4]int{1,2,3,4}
arreglo[4] = 5 // Error al compilar (index out of bounds)
```

```go
func modificar(arreglo [4]int) {
	arreglo[0] = 0
}

func main() {
	arreglo := [4]int{1,2,3,4}
	modificar(arreglo)
	fmt.Println(arreglo) // [1 2 3 4] No se pasa por referencia el arreglo
}
```

```go
func modificar(arreglo *[4]int) {
	arreglo[0] = 0
}

func main() {
	arreglo := [4]int{1,2,3,4}
	modificar(&arreglo)
	fmt.Println(arreglo) // [0 2 3 4] 
}
```

## Slices

- Reference Type
- Es dinámico. Puede variar su "tamaño"
- No contiene datos por sí mismo, es una referencia a un arreglo
- Tiene una longitud
- Tiene una **capacidad**: Longitud maxima del array al que se le hace referencia

```go
numeros := [6]int{1,2,3,4,5}
var slice []int = numeros[1:3]
fmt.Println(slice) // [2 3]

// formas de definir un slice

slice := []int{1,2,3,4,5}
fmt.Println(slice) // [1 2 3 4 5]

slice := []int{}
fmt.Println(slice) // []

slice := make([]int, 5, 10) // tipo, longitud, capacidad
fmt.Println(slice) // []
```

```go
s := []int{} // len=0 cap=0 []
s = []int{2,3,5,7,11,13} // len=6 cap=6 [2 3 5 7 11 13]
s = s[:4] // len=4 cap=6 [2 3 5 7]
s = s[1:] // len=3 cap=5 [3 5 7]
s = s[:5] // len=5 cap=5 [3 5 7 11 13]

s = s[:8] // Error en tiempo de compilación
```

```go
func modificar(slice []int) {
	slice[0] = 0
}

func main() {
	slice := []int{1,2,3,4}
	modificar(slice)
	fmt.Println(slice) // [0 2 3 4]
}
```