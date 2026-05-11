---
id: 1778191360-redes-de-flujo-y-algoritmo-de-ford-fulkerson
aliases:
  - Redes de Flujo y Algoritmo de Ford-Fulkerson
tags:
  - tda
---

# Redes de Flujo y Algoritmo de Ford-Fulkerson
## Redes de Flujo
- Podemos modelar con grafos flujos de materiales (ej cloacas, información en redes).
- El grafo es dirigido.
- Tenemos una (única) fuente, y un (único) sumidero (una única componente débilmente conexa). Fuente: Vértice con grado de entrada 0. Sumidero: vértice de grado de salida 0.
- Cada vértice intermedio simplemente traslada lo que le pasan. No produce ni consume.
- Cada arista tiene un peso que refleja la capacidad de transporte por esa vía.

![[Pasted image 20260507190618.png]]

Buscamos **maximizar** el flujo total.

### Restricciones
- No se aceptan bucles.
	- Si hay un bucle, lo sacamos.
- No pueden haber ciclos de dos vértices (aristas antiparalelas).
	- Agregamos un vértice ficticio para hacer un ciclo de tres vértices.
- Solo hay una fuente
	- Si hay mas de una fuente, agregamos una fuente común que salga a las dos fuentes originales con flujo infinito
- Solo hay un sumidero
	- Si hay mas de un sumidero, agregamos un sumidero al cuál se conecten los dos sumideros originales.

### Red Residual
Es el grafo con los mismos vértices, pero tiene como aristas:
1. Las mismas del original, al que aún les quede capacidad por utilizar. El peso es esa capacidad restante.
2. La arista opuesta, con peso la capacidad utilizada.
3. Si alguno de los anteriores es 0, no hay arista.

### Camino de aumento (*augmenting path*)
Si encontramos un camino de la fuente al sumidero en el grafo residual, entonces encontramos un camino por el que podemos aumentar el flujo.

Buscamos aumentar el flujo total, pero puede reducirse el que pasa por una arista en particular.

Vamos a usar BFS para encontrar este. 
## Algoritmo de Ford-Fulkerson
Esquema general:
```
def flujo(grafo, s, t):
	inicializamos el flujo por toda arista a 0
	Mientras haya un camino en la red residual:
		aumentamos el flujo acorde al camino
```

### ¿Cuál es la mejor forma de obtener un camino?
- Dependiendo de cómo se haga esto, puede no converger el algoritmo!
- Se hace con un BFS.

### Algoritmo
```python
def flujo(grafo, s, t):
	flujo = {}
	for v in grafo:
		for w in grafo.adyacentes(v):
			flujo[(v, w)] = 0
	grafo_residual = copiar(grafo)
	while (camino = obtener_camino(grafo_residual, s, t)) is not None:
		capacidad_residual_camino = min_peso(grafo_residual, camino)
		for i in range(1, len(camino)):
			if grafo.hay_arista(camino[i-1], camino[i]):
				flujo[(camino[i-1], camino[i])] += capacidad_residual_camino
			else:
				flujo[(camino[i], camino[i-1])] -= capacidad_residual_camino
			actualizar_grafo_residual(grafo_residual, camino[i-1], camino[i], capacidad_residual_camino)
	return flujo
	
**

def actualizar_grafo_residual(grafo_residual, u, v, valor):
	peso_anterior = grafo_residual.peso(u, v)
	if peso_anterior == valor:
		grafo_residual.remover_arista(u, v)
	else:
		grafo_residual.cambiar_peso(u, v, peso_anterior - valor)
	if not grafo_residual.hay_arista(v, u):
		grafo_residual.agregar_arista(v, u, valor)
	else:
		grafo_residual.cambiar_peso(v, u, grafo_residual.peso(v, u) + valor)
```

### Complejidad: $O(V*E^2)$

## Corte mínimo
El corte mínimo de una red es el peso total (mínimo) que necesitamos desconectar para que un grafo deje de estar conectado (conexo para grafos no dirigidos, débilmente conexo para dirigido).

Si el grafo es no pesado, corresponde a la cantidad de aristas (como considerar todos como peso = 1). 

Esto se aplica a cualquier tipo de grafo, pero para redes de flujo tenemos algo bastante interesante...

## Teorema: *max flow min cut*
Si el grafo corresponde a una red de flujo, entonces el corte mínimo tiene capacidad igual al flujo máximo.

Para que la fuente y el sumidero se encuentren en sets opuestos.

### ¿Cómo obtenemos el corte mínimo?
1. Agarramos nuestro grafo residual
2. Vemos todos los vértices a los que llegamos desde la fuente
3. Todas las aristas (del grafo original) que vayan de un vértice al que podamos llegar (en el residual) a uno que no (idem), son parte del corte.

## Teorema: Integer Value Flows
Si la red de transporte sólo tiene aristas con capacidades enteras, entonces existe un flujo máximo en el que la capacidad utilizada de cada arista es un número entero.

## Redes de flujo como técnica de diseño de algoritmos
### Aplicación I: Corte de vértices
Suponiendo red de flujo, ¿cuál es la mínima cantidad de vértices a sacar para que la fuente y el sumidero queden desconectados?

#### Transformación
Dado la red original:
- Para cada vértice intermedio (no fuente ni sumidero) transformar en 2 (entrada y salida). Arista de entrada a salida, peso 1
- Aristas originales -> de la salida del original a la entrada del original con peso "infinito".

![[Pasted image 20260507201336.png]]

![[Pasted image 20260507201348.png]]

### Aplicación II: Perfect Bipartite Matching
Dado un grafo no dirigido y bipartito, un match es un subconjunto de las aristas en el cual para todo vértice V a lo sumo una arista del match incide en V (en el match, tienen grado a lo sumo 1). Decimos que el vértice v está matcheado si hay alguna arista que incida en él (sino, está unmatcheado). El matching máximo es aquel en el que tenemos la mayor cantidad de aristas (matcheamos la mayor cantidad posible).

![[Pasted image 20260507202540.png]]

### Aplicación III: Disjoint Paths
Decimos que dos caminos son disjuntos si no comparten aristas (pueden compartir nodos).

Dado un grafo dirigido y dos vértices s y t, encontrar el máximo número de caminos disjuntos s-t en G.

> [!TODO]
> Revisar todas las aplicaciones

