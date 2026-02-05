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

## TDA LISAT
```go
type Lista[T any] interface {
	EstaVacia() bool
	InsertarPrimero(T)
	InsertarUltimo(T)
	BorrarPrimero() T
	VerPrimero() T
	VerUltimo() T
	Largo() int
	
	Iterar(visitar func(T) bool)
	Iterador() IteradorLista[T]
}
type nodoLista[T any] struct {
	dato T
	siguiente *nodoLista[T]
}

type listaEnlazada[T any] struct {
	primero *nodoLista[T]
	ultimo *nodoLista[T]
	largo int
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

Si $\log_b(a) = C$ -->  $T(n) =  O(n^c\log(n))$
Si $\log_b(a) < C$ -->  $T(n) =  O(n^c)$
Si $\log_b(a) > C$ -->  $T(n) =  o\!\left(n^{\log_b(a)}\right)$

## Ejercicio 3 primer recuperatiorio

El ejercicio nos propone utilizar RadixSort para ordenar los capítulos de unas series. Se quiere que quede ordenado primero por nombre de la serie, luego por temporada y por ultimo número de capitulo.

Para lograr esto, en el código debemos ordenar el arreglo primero por número de capitulo, luego ordenar el resultado por temporada, y por ultimo ordenar el resultado de este por nombre de la serie, en base a como debe funcionar RadixSort. 
Esto requiere un algoritmo de ordenamiento auxiliar. Para este caso, considero que el más adecuado es Counting Sort, ya que los 3 datos por el cual vamos a ordenar tienen tanto un rango acotado y conocido, como también son discretizables.

Primero ordenaremos el arreglo de capitulos por el número de capitulo. Para esto, debemos considerar el rango entre el capítulo con el número menor y el capítulo con el número mayor. Entonces, podemos determinar que el rango va a ser entre 1 y 9, es decir, un rango de 9.

Con esto, podemos armar el arreglo de frecuencias:
num de capitulo: [1 2 3 4 5 6 7 8 9]
frecuencia:            [3 1 1 0 1 0 0 1 1]

Luego de armar este arreglo, podemos proceder a armar el arreglo de los inicios de cada capitulo. Para determinar esto, debemos sumar la posicion del anterior inicio con la frecuencia del anterior elemento. (Por ejemplo, para determinar la posicion del 2, debemos sumar la posicion inicial del 1 (0) + su frecuencia (3) )

nums:  [1 2 3 4 5 6 7 8 9]
inicios: [0 3 4 4 5 5 5 6 7]

Por ultimo, armamos el arreglo ya ordenado. Para esto, recorremos el arreglo y vamos posicionando los valores en base a el valor de sus inicios. Por ejemplo, el capitulo 1 lo debemos posicionar en la posicion 0, ya que es donde se nos indica que inicia. Luego de esto, debemos sumar +1 al valor del inicio, asi si existe otro 1 no se sobreponga con el ya posicionado.

Este procedimiento hay que repetirlo dos veces mas, primero con el num de temporada y luego con el nombre de la serie (en este orden estrictamente)

Para comprender la complejidad del algoritmo, plantemos la ecuación de recurrencia:

## T(N) = O(d * (n + k))

- d: La cantidad de llamados al ordenamiento auxiliar
- n: Cantidad de elementos
- k: Rango
En este caso, como el rango de los capitulos, las temporadas y los nombres es diferente, debemos determinar lo siguiente:
- Capitulos: O(1*(n + 9))
- Temporada: O(1*(n + 3))
- Nombres: O(2*(n + 4))
Por lo tanto: T(N) = O(n+9) + O(n + 3) + O(n + 4)
En el caso que n sea muchisimo mas grande que sus respectivos k, el k se vuelve despreciable, por lo cual:
## T(N) = O(N)