
#algo2 
## Estructura

### Que es una estructura?

Una estructura (struct) permite en Go empaquetar variables de distinto tipo en un tipo nuevo.

```go
type Punto struct {
	X int
	Y int
}

var p Punto = Punto(X: 1, Y: 3) // Declaración e Inicialización
p = Punto(Y: 3) // No hace falta inicializar todos los campos
p = Punto(1, 3) // No hace falta mencionar el nombre de los campos

p.Y = 5 // Modifico el campo Y
p = Punto() // Se inicializa vacio
```

#### Con punteros

```go
var p *Punto = &Punto(X: 1, Y: 3)
p = &Punto(Y: 3)
p = &Punto(1, 3)
p.Y = 5
p = &Punto()
```

#### Modificar un campo

```go
func modificarPunto(p *Punto) {
	p.Y = 5
}

func main() {
	p := Punto(X: 3)
	modificarPunto(p)
	fmt.Println(p) // (3, 5) 
}
```

### Métodos

```go
func (p Punto) DistanciaAlOrigen() float64 {
	return math.Sqrt(float64(p.X*p.X + p.Y*p.Y))
}

func (p *Punto) Suma(otro Punto) Punto {
	return Punto(X: p.X + otro.X, Y: p.Y + otro.Y)
}

p1 := Punto(1,3)
p2 := &Punto(1,3)

p1.DistanciaAlOrigen()
p2.DistanciaAlOrigen()
p3 := p1.Suma(*p2)
p3 = p2.Suma(p1)
```

### Anidación

Se pueden anidar y referenciar otras estructuras.
Se puede incluir dentro de una estructura una referencia a sí misma (estructura recursiva)

```go
type Direccion struct {
	calle string
	numero int
}

type Persona struct {
	direccion Direccion
	nombre string
	padre, madre *Persona // Tiene que ser punteros porque nos tiraria un error 
						  // Al ser una estructura recursiva
}

jon := Persona{nombre: "Jon Voight"}
angie := Persona{
	Direccion{"Beverly Hills St.", 234},
	"Angelina Jolie",
	&jon,
	nil
}
```

```go
func (d *Direccion) String() string {
	return fmt.Sprintf("calle %s al %d", d.calle, d.numero)
}

func (p *Persona) Direccion() string {
	return fmt.Sprintf("%s vive en %s", p.nombre, p.dir)
}

fmt.Println(angie.Direccion())
```

## Errores

### Cómo usar errores

```go
import (
	"fmt"
	"fmtconv"
)

func main() {
	str := "asd"
	entero, err := strconv.Atoi(str)
	if err != nil {
		fmt.Printf("No se pudo convertir: %v\n", err)	
	} else {	
		fmt.Println("El entero es:", entero)
	}
	// fmt.Println("El entero es:", entero) // --> ? (No se sabe que devuelve)
}
```

```go
func Index(slice []int, e int) (int, error) {
	for indice, valor := range slice {
		if valor == e {
			return indice, nil
		}
	}
	return 0, errors.New("no se encontró el elemento")
}

numeros := []int{1,2,3,4,5}
indice, err := Index(numeros, 6)
if err != nil {
	fmt.Printf("No se pudo encontrar: %v\n", err)
} else {
	fmt.Println("El indice es:", indice)
}
```

## Strings

Una cadena es un slice de `bytes` de sólo lectura (no se pueden modificar)

Cada "caracter" de un string es de tipo `rune`. Para representar cualquier símbolo Unicode cada rune puede ocupar entre 1 y 4 bytes

El encoding de las cadenas es siempre UTF-8

```go
import "fmt"

func main() {
	var e rune
	for _, e = range "今日は Algo2 ✌" {
		fmt.Printf("Símbolo %d código Unicode %d\n", e, e)	
	}
}
```

```go
func main() {
	cadena := "今日は Algo2 ✌"
	runes := []rune(cadena)
	for i := range runes {
		fmt.Printf("Posicion %d: %c\n", i, runes[i]) // Posicion 0: 今 	
	}
}
```


## Archivos

### Leer input de usuario
```go
import {
	"bufio"
	"fmt"
	"os"
}

func main() {
	fmt.Println("Ingrese un input")
	s := bufio.NewScanner(os.Stdin)
	s.Scan()
	fmt.Printf("Lei: %s\n", s.Text())
}
```

### Leer de un archivo

```go
const ruta = "archivo.txt"

func main() {
	archivo, err := os.Open(ruta)
	if err != nil {
		fmt.Printf("Error %v al abrir el archivo %s", ruta, err)	
	}
}
```
