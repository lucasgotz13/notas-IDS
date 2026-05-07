
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

## TDA LISTA
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

## T(N) = O(d * (n + k))

- d: La cantidad de llamados al ordenamiento auxiliar
- n: Cantidad de elementos
- k: Rango
## Counting sort
```go
func countingSort(arr []string, digito int) []string {
	frecuencias := make([]int, 10)
	for _, elem := range arr {
		val := strconv.Atoi(string(elem[digito]))
		frecuencias[pos]++
	}
	
	inicios := make([]int, 10)
	for i := 1; i < len(frecuencias); i++ {
		inicios[i] = inicios[i - 1] + frecuencias[i - 1]
	}
	
	res := make([]int, len(arr))
	for _, elem := range arr {
		val := strconv.Atoi(string(elem[digito]))
		pos := inicios[val]
		res[pos] = elem
		inicios[val]++
	}
	return arr
}
```

# Diccionario
## Struct hash abierto
```go
type hashAbierto[K, V any] struct {
	tabla Lista[campoHash[K, V]]
	cantidad int	
	largo int
	cmp func (K, K) bool
}
type campoHash[K comparable, V any] struct {
	clave K
	valor V
}
```
## Struct hash cerrado
```go
type hashCerrado[K comparable, V any] struct {
	tabla []celdaHash[K,V]
	cantidad int
    largo int
	borrados int
	cmp func (K, K) bool
}

type celdaHash[K comparable, V any] struct {
	clave K
	valor V
	estado estadoParClaveDato // (VACIO, BORRADO o OCUPADO)
}
```

## Primitivas
- Guardar(clave, valor)  --> O(1)
- Pertenece(clave) bool  --> O(1)
- Obtener(clave) V  --> O(1)
- Borrar(clave) V  --> O(1)
- Cantidad  --> O(1)
# Arboles
## Definiciones
- Nodo interno --> Los que tienen hijos
- Hojas --> Los que no tienen hijos
## Caso base para las funciones:
```go
if ab == nil {
	return
}
```
### Struct (AB)
```go
type ab[T any] struct {
	izq *ab[T]
	der *ab[T]
	dato T
}
```
## ABB
- **Propiedad**: Todo lo que esta a la izq es menor a la raíz y todo lo que esta a la derecha es mayor a la raíz
- Todas sus primitivas son O(log n)
### Struct
```go
type ABB[K comparable, V any] struct {
	raiz *nodoAbb[K, V]
	cantidad int
	cmp func(K, K) int
}
```
### Primitivas
- Guardar(clave, valor)
- Obtener(clave) V
- Pertenece(clave) bool
- Borrar(clave) V
- IterInterno
- Iterador() --> O(log n) al crear, despues O(n)
- Cantidad() V --> O(1)
## Recorridos:
### Preorder:
Primero el padre, luego el izq y luego der
### Inorder:
Primero izq, luego el padre, luego der
### Postorder:
Primero izq, luego der, luego el padre
### Niveles:
Se recorre tipo BFS
## AVL
## Propiedades
- Tiene que cumplir la propiedad de ABB
- abs(h_izq - h_der) <= 1
![[Pasted image 20251009191655.png]]
# Heap
## Propiedades
- Todo nodo es mas grande que sus dos hijos
- El arbol (visual) tiene que ser izquierdista
  Padre(i) = (i - 1) / 2
  hijo_izq = 2 x i + 1
  hijo_der = 2 x i + 2
## Struct
```go
type heap[T any] struct {
	datos []T
	cantidad int
	cmp func(T, T) int
}
```
## Primitivas
- VerMax() T --> O(1)
- Encolar(T) --> O(log n)
- Desencolar() T --> O(log n)
- Cantidad() int --> O(1)
- EstaVacia() bool --> O(1)

- upheap: O(log n)
- downheap: O(log n)
- Heapify: O(n)
# Grafos
Se componen de
- V: Cantidad de vértices
- E: Cantidad de aristas

## Tipos de grafos
- Grafos dirigidos: Las aristas tienen una dirección asociada (Vértice de origen y vértice de destino)
- Grafos no dirigidos: Es una relación **bidireccional** (No hay origen o fin)
- Con peso: Tienen un valor asociado
- Sin peso: No tienen ninguno

## Listas de adyacencia
### Diccionario de Diccionario
```javascript
{
A: {B: "", D: ""},
B: {C: ""},
C: {},
D: {}
}
```


|                   | Memoria  |    Agregar vértice     | Agregar arista | Ver si A --> B | Sacar vértice | Sacar arista |
| :---------------: | :------: | :--------------------: | :------------: | :------------: | :-----------: | :----------: |
| Matriz incidencia | O(V X E) |          O(E)          |      O(V)      |      O(E)      |   O(V x E)    |   O(V x E)   |
| Matriz adyacencia |  O(V²)   |      O(V) (redim)      |      O(1)      |      O(1)      |     O(1)      |     O(1)     |
| Lista adyacencia  | O(V + E) | - OLL (V)<br>- ODL (1) |      O(V)      |      O(V)      |   O(V + E)    |     O(V)     |
| LA: dict de dict  |  O(V+E)  |          O(1)          |      O(1)      |      O(1)      |     O(V)      |     O(1)     |
*OLL: Lista de lista*
*ODL: Diccionario de lista*

## Definiciones
- Camino (simple): Cualquier secuencia de vertice que siga aristas
- Ciclo: Camino simple que se cierra al empezar por el mismo vertice de antes. Tiene que usar dos aristas diferentes
- Componente conexa (no dirigidos): Todo vertice se puede conectar a otro de forma directa o indirecta
- Componente debilmente conexa: Si saco las direcciones, que componentes conexas me quedan
- Componente fuertemente conexa: Conjunto de vértices que se unen todos con todos (directa o indirectamente)
## Recorridos
### BFS (Breath-First search)
En un arbol también es conocido como el recorrido por niveles
```python
def bfs(grafo, origen):
	visitados = set()
	padres = {}
	orden = {}
	q = Cola()
	visitados.add(origen)
	padres[origen] = None
	orden[origen] = 0
	q.Encolar(origen)
	while cola:
		v = q.Desencolar()
		for w in grafo.adyacentes(v):
			if w not in visitados:
				visitados.add(w)
				padres[w] = v
				orden[w] = orden[v] + 1
				q.Encolar(w)
	return padres, orden
```
### DFS (Depth-first search)
```python
def _dfs(grafo, v, visitados, padres, orden):
	visitados.add(v)
	for w in grafo.adyacentes(v):
		if w not in visitados:
			padres[w] = v
			orden[w] = orden[v] + 1
			_dfs(grafo, w, visitados, padres, orden)


def dfs(grafo, v):
	visitados = set()
	orden = {}
	padres = {}
	for v in grafo:
		if v not in visitados:
			orden[v] = 0
			padres[v] = None
			_dfs(grafo, v, visitados, padres, orden)
	return padres, orden	
```
**Complejidad de ambos recorridos: O(V+E)**

## Orden topológico
### Por BFS
1. Obtenemos los grados de entrada de cada vertice
2. Los que tengan g_ent = 0 los encolamos
3. Cada vez que desencolamos un vértice, le restamos 1 a los g_ent de cada adyacente. Si algun g_ent de un adyacente llega a 0, lo encolamos
4. Cuando no hay mas nada para desencolar, se termina el algoritmo
### Por DFS
1. Se hace el típico DFS
2. Cuando terminamos de analizar un vértice, lo apilamos
3. Damos vuelta el orden de la pila
DFS tiene mas utilidad si tenemos que ir de vértice en vértice
## Arboles de tendido minimo
### Propiedades
- Árbol --> Acíclico
- Contiene todos los vértices del grafo original
- La sumatoria de todas las aristas necesarias para llegar a todos los vértices tiene que ser la mínima posible
### Algoritmo de prim
1. Empezamos en un vértice aleatorio
2. Meto todas las aristas (cuyo destino no fue visitado) en el heap
3. Voy sacando del heap (por menor peso) y agrego a la solución si el destino no esta visitado
4. Repito paso 2
```python
def mst_prim(grafo):
    v = random.choice(grafo.keys())
    visitados = set()
    visitados.add(v)
    q = Heap()
    for w in grafo.adyacentes(v):
        q.encolar((v, w), grafo.peso(v, w))
    arbol = Grafo(es_dirigido=False, lista_vertices=grafo.obtener_vertices())
    while not q.esta_vacio():
        (v, w), peso = q.desencolar()
        if w in visitados:
            continue
        arbol.agregar_arista(v, w, peso)
        visitados.add(w)
        for x in grafo.adyacentes(w):
            if x not in visitados:
                q.encolar((w, x), grafo.peso(w, x))
    return arbol
```
### Algoritmo de Kruskal
1. Ordenamos todas las aristas por peso
2. Recorremos las aristas. Si estas no cierran un ciclo las agregamos (Se va a cerrar un ciclo cuando los 2 vértices de la arista ya forman una componente conexa)
Ventaja de Kruskal: Puede obtener el MST de varias componentes conexas
```python
def obtener_aristas(grafo):
    aristas = []
    visitados = set()
    for v in grafo:
        for w in grafo.adyacentes(v):
            if w not in visitados:
                aristas.append((v, w, grafo.peso(v, w)))
        visitados.add(v)
    return aristas


PESO = 2


def mst_kruskal(grafo):
    conjuntos = UnionFind(grafo.obtener_vertices())
    aristas = sorted(obtener_aristas(grafo)) # ordeno de menor a mayor por peso de las aristas
    arbol = Grafo(False, grafo.obtener_vertices())
    for a in aristas: # > O(E log V)
        v, w, peso = a
        if conjuntos.find(v) == conjuntos.find(w):
            continue
        arbol.arista(v, w, peso)
        conjuntos.union(v, w)
    return arbol
```

Complejidad de ambos algortitmos: **O(E log V)**

## Aplicaciones del DFS
### Puntos de articulación
En un grafo no dirigido, son los vértices que si se remueven, el grafo deja de ser conexo

¿Cómo los detectamos? => Algoritmo de Tarjan
1. Aplicamos DFS, viendo las aristas de retorno
2. Si el vértice raíz del recorrido tiene más de 1 hijo => es PA
3. Si el vértice no es raíz, y algunos de sus hijos no tiene forma de "ir mas abajo" por otro camino, es PA
Si mb[v] >= orden[w] --> w es PA
```python
def dfs_puntos_articulacion(grafo, v, visitados, padre, orden, mas_bajo, ptos, es_raiz):
    hijos = 0
    mas_bajo[v] = orden[v]
    for w in grafo.adyacentes(v):
        if w not in visitados:
            hijos += 1
            orden[w] = orden[v] + 1
            padre[w] = v
            visitados.add(w)
            dfs_puntos_articulacion(grafo, w, visitados, padre, orden, mas_bajo, ptos, es_raiz=False)

            # Lo siguiente se ejecuta una vez ya aplicado a W, y recursivamente a sus hijos
            if mas_bajo[w] >= orden[v] and not es_raiz:
                # No hubo forma de pasar por arriba a este vertice, es punto de articulacion
                # se podría agregar como condicion "and v not in ptos" (ya que podria darse por mas de una rama)
                ptos.add(v)
            # Al volver me quedo con que puedo ir tan arriba como mi hijo, si es que me supera
            mas_bajo[v] = min(mas_bajo[v], mas_bajo[w])
        elif padre[v] != w: # evitamos considerar a la arista con el padre como una de retorno
            # Si es uno ya visitado, significa que puedo subir (si es que no podia ya ir mas arriba)
            mas_bajo[v] = min(mas_bajo[v], orden[w])

    if es_raiz and hijos > 1:
        ptos.add(v)


def puntos_articulacion(grafo):
    origen = grafo.random()
    origen = "A"
    puntos_articulacion = set()
    dfs_puntos_articulacion(grafo, origen, {origen}, {origen: None}, {origen: 0}, {}, puntos_articulacion, True)
    return puntos_articulacion
```
### Detección de CFCs
Algoritmo de Tarjan para detectar CFCs:
1. Aplicamos DFS viendo las aristas de retorno
2. Vamos apilando los vértices en una pila
3. Si al recorrer todos los adyacentes el más bajo es igual a su orden, se cierra un cfc y desapilamos de la pila hasta encontrar a este mismo.
```python
def dfs_cfc(grafo, v, visitados, orden, mas_bajo, pila, apilados, cfcs, contador_global):
    orden[v] = mas_bajo[v] = contador_global[0]
    contador_global[0] += 1
    visitados.add(v)
    pila.apilar(v)
    apilados.add(v)
    for w in grafo.adyacentes(v):
        if w not in visitados:
            # llamamos recursivamente
            dfs_cfc(grafo, w, visitados, orden, mas_bajo, pila, apilados, cfcs, contador_global)
        if w in apilados:
            # Nos tenemos que fijar que este entre los apilados y que no estemos viendo a un vertice visitado
            # en otro dfs hecho antes --> no son parte de la misma CFC porque habrian sido visitados en el mismo DFS
            mas_bajo[v] = min(mas_bajo[v], mas_bajo[w])

    if orden[v] == mas_bajo[v]:
        # Se cumple condicion de cierre de CFC, armamos
        nueva_cfc = []
        while True: # porque python no tiene un do-while
            w = pila.desapilar()
            apilados.remove(w)
            nueva_cfc.append(w)
            if w == v:
                break
        cfcs.append(nueva_cfc)


def cfcs_grafo(grafo):
    resultados = []
    visitados = set()
    for v in grafo:
        if v not in visitados:
            dfs_cfc(grafo, v, visitados, {}, {}, Pila(), set(), resultados, [0])
    return resultados
```
