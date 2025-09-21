#algo2 


## TDA PILA

```go
type Pila[T any] interface {
	Apilar(T)
	Desapilar() T
	VerTope() T
	EstaVacia() bool
}

type pilaDinamica[T any] struct {
	datos []T
	cantidad int
}

func (pila *pilaDinamica) EstaVacia() bool {
	return pila.cantidad == 0
}

func (pila *pilaDinamica) VerTope() T {
	if pila.cantidad == 0 {
		panic()
	}
	return pila.datos[pila.cantidad - 1]
}

func (pila *pilaDinamica) redimensionar(tamanio int) {
	nuevosDatos := make([]T, tamanio)
	copy(nuevosDatos, pila.datos)
	pila.datos = nuevosDatos
}

func (pila *pilaDinamica) Apilar(elem T) {
	if pila.cantidad == len(pila.datos) {
		pila.redimensionar(len(pila.datos) * _MITAD)
	}
	pila.datos[pila.cantidad] = elem
	pila.cantidad++
}

func (pila *pilaDinamica) Desapilar() T {
	if pila.cantidad == 0 {
		panic()
	}
	if pila.cantidad*4 <= len(pila.datos) {
		pila.redimensionar(len(pila.datos) / _MITAD)
	}
	pila.cantidad--
	elem := pila.datos[pila.cantidad]
	return elem
}
```

## TDA COLA
```go
type Cola[T any] interface {
	Encolar(T)
	Desencolar() T
	VerPrimero() T
	EstaVacia() bool
}

type nodo[T any] struct {
	dato T
	prox *nodo[T]
}

type colaEnlazada[T any] struct {
	primero *nodo[T]	
	ultimo *nodo[T]
}

func CrearNodo[T any](elem T) *nodo[T] {
	nodo := &nodo[T]{dato: elem}
	return nodo
}

func (cola *colaEnlazada) EstaVacia() bool {
	return cola.primero == nil
}

func (cola *colaEnlazada) VerPrimero() T {
	if cola.primero == nil {
		panic()	
	}
	return cola.primero.dato
}

func (cola *colaEnlazada) Encolar(elem T) {
	nodoNuevo := CrearNodo(elem)
	if cola.primero == nil {
		cola.primero = nodoNuevo
	} else {
		cola.ultimo.prox = nodoNuevo
	}
	cola.ultimo = nodoNuevo
}

func (cola *colaEnlazada) Desencolar() T {
	if cola.primero == nil {
		panic()	
	}
	elem := cola.primero.dato
	cola.primero = cola.primero.prox
	if cola.primero == nil {
		cola.ultimo = nil
	}	
	return elem
}
```
## Enums
```go
type Genero int

const (
	Terror Genero = iota
	Comedia
	Tragedia
	
)
```

## Teorema maestro

Teniendo la ecuacion:
#### $T(n) = A \, T\!\left(\tfrac{n}{B}\right) + O(n^c)$

- A: Cantidad de llamados recursivos
- B: Proporción del tamaño original con el que llamamos recursivamente
- C: (Todo lo que no son llamados recursivos)

#### Si $\log_b(a) = C$ -->  $T(n) =  O(n^c\log(n))$
#### Si $\log_b(a) < C$ -->  $T(n) =  O(n^c)$
#### Si $\log_b(a) > C$ -->  $T(n) =  o\!\left(n^{\log_b(a)}\right)$
