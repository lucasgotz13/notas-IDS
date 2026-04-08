---
id: 1774562671-fuerza-bruta-y-backtracking
aliases:
  - Fuerza Bruta y Backtracking
tags:
  - tda
---

# Fuerza Bruta y Backtracking

- [[#Fuerza Bruta|Fuerza Bruta]]
- [[#Backtracking|Backtracking]]
	- [[#Backtracking#Ejemplo 1 - N reinas|Ejemplo 1 - N reinas]]
	- [[#Backtracking#Ejemplo 2 - Independent Set|Ejemplo 2 - Independent Set]]
		- [[#Ejemplo 2 - Independent Set#Código (por Fuerza Bruta)|Código (por Fuerza Bruta)]]
		- [[#Ejemplo 2 - Independent Set#Código (por Backtracking)|Código (por Backtracking)]]
		- [[#Ejemplo 2 - Independent Set#Complejidad|Complejidad]]
	- [[#Backtracking#Ejemplo 2b - variante|Ejemplo 2b - variante]]
	- [[#Backtracking#Ejemplo 3 - Camino Hamiltoniano|Ejemplo 3 - Camino Hamiltoniano]]

## Fuerza Bruta
Tenemos un problema combinatorio => Probamos todas las soluciones
Ejemplo: Ordenar => O(n!)

Sin embargo, a veces no nos queda de otra => Ejemplo: Queen's Gambit

## Backtracking
Cuando sabemos que una combinación parcial que ya construimos no va a llevar a un resultado válido, *podamos*.


> [!Info]- Receta "rápida" de Algoritmo backtracking
> 1. Si ya encontre una solucion, la devuelvo y termino.
>2. Avanzo si puedo
>3. Pruebo si la solución parcial es válida
>4. Si no lo es, retrocedo y vuelvo a 2)
>5. Si lo es, llamo recursivamente y vuelvo a 1)
>6. Si llegue hasta aca, ya probe con todo y no encontre una solucion
>No funciona para todos los casos.

Para el caso de grafos, hay 2 tipos de resoluciones:
- Ir moviéndonos sin un recorrido.
- Hacerlo con DFS (si nos importa el camino), desmarcando los visitados cuando **no hay solución "por este camino"**.

> [!Warning] Al podar estamos limitando la recursividad

### Ejemplo 1 - N reinas
Dado un tablero de ajedrez NxN, ubicar (si es posible) a N reinas de tal manera que ninguna pueda *comerse* con ninguna.

### Ejemplo 2 - Independent Set

Quiero guardar en los V vértices de un grafo, un número K de elementos. Debo elegir un total de K vértices en los cuales guardar los elementos. Restricción! Queremos ver de ubicar los K elementos en vértices, sin que hayan dos vértices adyacentes con elementos.

Con Backtracking, probamos todas nuestras opciones en cada paso en el que estoy => En cada vértice, nuestras opciones son: ¿Guardo el elemento acá, o no?

#### Código (por Fuerza Bruta)
```python
def _ubicacion_FB(grafo, vertices, v_actual, puestos, k):
   if len(puestos) == k:
       return puestos if es_compatible(grafo, puestos) else None
   if v_actual == len(grafo):
       return None

  


   # Mis opciones son poner acá, o no
   puestos.add(vertices[v_actual])
   solucion = _ubicacion_FB(grafo, vertices, v_actual + 1, puestos, k)
   if solucion != None:
       return solucion
   puestos.remove(vertices[v_actual])
   return _ubicacion_FB(grafo, vertices, v_actual + 1, puestos, k)**

def es_compatible(grafo, puestos):
    for v in puestos:
        for w in puestos:
            if v == w: continue
            if grafo.hay_arista(v, w):
                return False
    return True
```


> [!Info]- Comentarios
> Cuando yo vuelva para atrás, yo tengo que dejar el estado de la cosa como antes de invocar la función.
> Las podas se ponen después de los casos base o antes de las funciones recursivas


#### Código (por Backtracking)
```python
def _ubicacion_BT(grafo, vertices, v_actual, puestos, n):
    if len(puestos) == n:
        return puestos if es_compatible(grafo, puestos) else None
    if v_actual == len(grafo):
        return None

  

    if not es_compatible(grafo, puestos) or ya_no_llego(grafo, vertices, v_actual, puestos):
        return None
    # Mis opciones son poner acá, o no
    puestos.add(vertices[v_actual])
    solucion = _ubicacion_BT(grafo, vertices, v_actual + 1, puestos, n)
    if solucion != None:
        return solucion
    puestos.remove(vertices[v_actual])
    return _ubicacion_BT(grafo, vertices, v_actual + 1, puestos, n)**	
	
def es_compatible(grafo, puestos, ultimo_puesto):
    for w in puestos:
        if ultimo_puesto == w: continue
        if grafo.hay_arista(ultimo_puesto, w):
            return False
    return True
```

#### Complejidad
- Fuerza Bruta: O($2^n$)
- Backtracking: Misma complejidad, pero mejores tiempos de ejecución

### Ejemplo 2b - variante
En vez de devolver una opción, devolver todas las opciones viables.
No podemos parar en cuanto encontremos una.

### Ejemplo 3 - Camino Hamiltoniano

> [!Info]- Definicion
> Un camino hamiltoniano, en el campo matemático de la teoría de grafos, es un camino de un grafo, que visita todos los vértices del grafo una sola vez. Si además el último vértice visitado es adyacente al primero, el camino es un ciclo hamiltoniano.

[Diapositiva](https://docs.google.com/presentation/d/1rszx1zlfm7sGA98Tabcq22KbDBvfrYOJ6G_QZgDFnRc/edit?slide=id.g1dceb505b08_0_136#slide=id.g1dceb505b08_0_136)


> [!TODO] Ver ejercicio resuelto de Backtracking de la guía
