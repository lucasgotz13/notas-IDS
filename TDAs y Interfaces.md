#algo2
# TDA (Tipo de Dato Abstracto)

-  Es un conjunto de valores y de operaciones definidos mediante una especificación independiente de cualquier representación
-  La manipulación de un TDA sólo depende de su especificación, nunca de su implementación
### Ejemplo: **Puerta**

#### Primitivas (lado usuario):
- **Abrir**
- **Cerrar**
- **estaAbierta**

### Lo importante de un TDA
- Solamente se trabaja con las primitivas del TDA
- Nunca se tiene que programar código que dependa de la implementación interna de un TDA
- No se puede acceder a los atributos internos

#### Lado implementación
```go
type Puerta struct {
	estado int
}

func (puerta *Puerta) cerrar() {
	puerta.estado = 0	
}
```

## Invariantes de las primitivas
- Sirven para especificar al TDA y son parte de la descripción de una primitiva
- Componen las precondiciones y postcondiciones de cada primitiva
- Ejemplo: una invariante de la primitiva abrir() "luego de aplicar abrir(), el estado de la puerta será abierta"

# Interfaces
### Interfaz pública vs Implementación

Interfaz pública: El lugar donde se **define** el TDA (Qué dice que hace)
Implementación: Como se **implementa** el TDA (Como lo hace)

## Qué es una interfaz?
- Un conjunto de firmas de primitivas
- Es un contrato entre la persona que va a implementar el TDA y la persona que lo va a consumir
- Uno de los objetivos es el de enmascarar implementaciones concretas

### Sintaxis
```go
type figura interface {
	// Calcula el area de la figura
	area() float64
	
	// Calcula el perimetro de la figura
	perimetro() float64
}

type rect struct {
	acho, alto float64
}

type circulo struct {
	radio float64
}
```
#### Implementación
```go
func (r rect) area() float64 {
	return r.ancho * r.alto
}

func (r rect) perimetro() float64 {
	return 2*r.ancho + 2*r.alto
}

func (c circulo) area() float64 {
	return Math.Pi * c.radio * c.radio
}

func (c circulo) perimetro() float64 {
	return 2 * math.Pi * c.radio
}
```

```go
func medidas(g figura) {
	fmt.Println(g)
	fmt.Println(g.area())
	fmt.Println(g.perimetro())
}

func main() {
	r := rect{ancho: 3, alto: 4}
	c := circulo{radio: 5}
	
	medidas(r)
	medidas(c)
}
```
- Nunca vamos a usar la implementación concreta directamente
- Para ello vamos a no exportar los tipos concretos que implementan las interfaces
- El paquete que contiene la implementación nos debe brindar una función que cree una implementación concreta pero que devuelva la interfaz -> Esto es lo que vamos a exportar.
```go
// ../puerta.go
type Puerta interface {
	Abrir()
	Cerrar()
	EstaAbierta() bool
}
```
```go
// ../puerta_impl1.go
type puertaImplInt struct {
	estado int
}
func CrearPuerta() Puerta {
	return &puertaImplInt{}
}

func (puerta1 *puertaImplInt) Abrir() {
	puerta.estado = 0
}

func (puerta1 *puertaImplInt) Cerrar() {
	puerta.estado = 1;
}

func (puerta1 *puertaImplInt) EstaAbierta() bool {
	return puerta.estado == 0;
}
```
### Conclusión
- La interfaz contiene la **declaración** de las primitivas de nuestro TAD
	- Cuales son los nombres de las primitivas disponibles?
	- Qué reciben? Qué devuelven?
	- Qué hacen?

## Ejemplo completo: Vector

Definamos un TDA Vector que permita:
- Modificar el elemento en una posicion indicada
- Insertar al final (append)
- Eliminar el último elemento
- Eliminar un elemento arbitrario

```go
func CrearVector(tam int) Vector {
	vector := new(miVector)
	vector.datos = make([]int, TAM_INICIAL)
	vector.cant = 0
	return vector
}

func (vector *miVector) Obtener(pos int) int {
	if pos >= vector.cant {
		panic("Fuera de rango")
	}
	return vector.datos[pos]
}

func (vector *miVector) Modificar(pos int, valor int) {
	if pos >= vector.cant {
		panic("Fuera de rango")	
	}
	vector.datos[pos] = valor
}

func (vector *miVector) redimensionar(tam int) { // aspecto interno del TDA
	nuevosDatos := make([]int, tam)
	copy(nuevosDatos, vector.datos)
	vector.datos = nuevosDatos
}
```
###  Interface: Error
```go
// Provisto por el lenguaje
type error interface {
	Error() string
}
```
```go
type DivisionPorCeroError struct {}
func (e DivisionPorCeroError) Error() string {
	return "No se puede dividir por cero"
}
```
```go
type ConexionError struct {
	ip IP
}

func (e ConexionError) Error() {
	return fmt.Sprintf("No se pudo conectar con %s", e.ip)
}
```

```go
func main() {
	..., err := ...
	switch v := err.(type) {
		case DivisionPorCeroError:
			...
		case ConexionErorr:
			...
		default:
			...	
	}
}
```
### Interfaces: any

*any*: interfaz vacía, puede contener cualquier tipo

```go
var a any = "3"
var b any = 3
var c any = Punto(3,6)
```

Podría usar `any` para tener un TDA que acepte cualquier tipo

#### Ejemplo
```go
type Pila interface {
	Apilar(e any)
	Desapilar() any
}

p = crearPila()
p.Apilar(5)
p.Apilar("3")

e := p.Desapilar()
```

### Interfaces: Casteo
```go
func f () figura {
	...
}
```
```go
figura := f()
var figuraCirculo circulo = figura.(circulo) // panic: interface conversion: interface () is rect, not circulo
```
```go
figura := f()
circulo, ok := figura.(circulo)
if !ok {} // manejo el error
```
# Error vs Panic

`panic` se debe usar cuando hay un error irrecuperable o excepcional en la ejecución
`error` se debe usar  cuando es **esperable** que algo pueda fallar




