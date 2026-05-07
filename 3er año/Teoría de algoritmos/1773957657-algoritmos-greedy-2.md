---
id: 1773957657-algoritmos-greedy-2
aliases:
  - algoritmos-greedy-2
tags:
  - tda
---

# Algoritmos Greedy (parte 2)

## Problema de la mochila

Tenemos una mochila con una capacidad W (peso, volumen). Hay elementos a guardar. Cada elemento tiene un peso y un valor. Queremos maximizar el valor de lo que nos llevamos sin pasarnos de la capacidad.

¿Solución? => **No hay una solución definitiva utilizando algoritmos greedy (hay aproximaciones)**

### Problema de la mochila 2
Ahora supongamos que no es necesario poner "todo un elemento" sino que podemos poner proporciones.

¿Ahora un algoritmo greedy sería óptimo?

## Problema de Scheduling 2

Ahora tenemos tareas con un deadline (fecha límite) $d_{i}$ y una duración $t_i$, pero pueden hacerse en cualquier momento, siempre que se hagan antes del deadline. Si se hacen después del deadline, incurrimos en una latencia.

Para este problema, buscamos minimizar la latencia máxima en el que las tareas se ejecuten. Es decir, si definimos que una tarea $i$ empieza en $s_i$, entonces termina en $f_{i} = s_{i} * t_{i}$ y su latencia es $L_{i} = f_{i} - D_{i}$ (si $f_{i} > d_{i}$, sino 0).

El tiempo que me va a tomar hacer todas las tareas es fijo.

### Demostración por inversiones

Ordenar por Deadline nos da una propuesta de solución.

Necesitaríamos probar que está solución es igual de buena que cualquier hipotética solución óptima.

Podemos realizar inversiones sobre la solución óptima, sin alterar su optimalidad, para demostrar la equivalencia con nuestra solución propuesta.

#### Inversión
Decimos que un schedule tiene una inversión si dentro de ese schedule tenemos dos elementos s[i] y s[j] tal que i < j pero $d_{i}$ > $d_{j}$ (en criollo, un elemento con deadline posterior viene antes que uno con deadline anterior, entre sí)

Postulado: Todos los schedules posibles sin inversiones (y sin tiempo en desuso) tienen la misma latencia máxima. 

Demostración: por no tener inversiones, sólo pueden variar la posición de tareas que tengan mismo deadline, y van a tener que ser consecutivas. La última de estas tareas es la que tiene mayor latencia entre ellas, y esta latencia no depende del orden de las tareas.

![[Pasted image 20260319203522.png]]


> [!TODO] Revisar ejercicio de exámen

## Generación de un grafo
Dado una lista de n números naturales, implementar un algoritmo en tiempo polinomial que cree un grafo de n nodos cuyos grados sean los indicados por esa lista. G debe ser simple y sin bucles.
### Solución
1. Creamos un grafo con cantidad de nodos igual al largo del arreglo.
2. Ordenamos la lista de grados de mayor a menor asignando un índice dependiendo de la posición en el arreglo ordenado.
3. Mientras haya aristas para colocar:
	a. Tomamos el valor del grado del vértice de menor grado y lo denominamos k.
	b. Creamos una arista entre los k vértices con mayor grado y el vértice de menor grado
	c. Restamos el grado en cada uno de los k vértices de mayor grado
	d. Eliminamos al vértice de menor grado del arreglo
	e. Ordenamos el arreglo para que se mantenga el orden, si es necesario.
4. Si el arreglo queda vacío, devolvemos la asignación
	a. Si queda alguno, indicamos que falló.

Regla greedy: En cada iteración, resolver un vértice

> [!TODO] Ver la regla greedy
