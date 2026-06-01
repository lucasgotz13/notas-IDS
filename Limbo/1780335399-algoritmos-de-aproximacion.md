---
id: 1780335399-algoritmos-de-aproximacion
aliases:
  - Algoritmos de Aproximacion
tags:
  - tda
---

# Algoritmos de Aproximacion

- Diseñados para correr en tiempo polinomial
- Encuentran soluciones que _garantizan_ estar cerca del óptimo
- Se puede demostrar que encontramos solución cerca del óptimo

## Metodologías para los algoritmos de aproximación

- Algoritmos Greedy
- Pricing method
- Programación lineal, --- y programación Entera
- Programación dinámica y ---

## Problema de Balanceo de Carga

Dadas m Máquinas y un conjunto n de trabajos, donde cada trabajo j toma un tiempo $t_j$, se desea asignar el trabajo en las Máquinas de forma balanceada.
Dada una asignación A(i) para la Máquina i, su tiempo de trabajo es

$$
T_i = \sum_{j \in A(i)} t_j
$$

Y queremos encontrar la asignación que minimice el máx valor de $T_i$, que también representa el tiempo que se tardará en finalizar todos los trabajos
El Problema de Balanceo de Carga es NP-difícil

### Metodología 1: Greedy

- Iterar sobre todos los trabajos
- Para cada trabajo, asignarlo a la máquina con menos trabajo al momento.
- Ordenar de mayor a menor podría servir, pero hay que hacer algo mas.

#### Análisis de la solución greedy

- Tocaría comparar nuestra solución T con la solución óptima T\*
- No conocemos la solución T\* óptima
- La mejor asignación posible sería repartir para que cada máquina haga exactamente la misma cantidad de trabajo
  $$
  T* \geq \frac{1}{m} \sum_{j} T_j
  $$
- Además, nunca se puede terminar antes que el trabajo mas largo.
  $$
  T* \geq max_j t_j
  $$

#### Demostración: cuánto nos aproximamos

- Necesitamos comparar nuestra solución T con lo que sabemos del óptimo.
- Una de nuestras máquinas en T tuvo más carga que cualquier otra.
- Habrá habido un último trabajo $T_j$ en ser colocado en esa máquina
- Si ese trabajo $T_j$ no es muy grande, entonces podemos acotar con $T* \geq \frac{1}{m} \sum_{j} T_j$
- Si ese trabajo $T_j$ es bastante grande, usamos $T* \geq max_j t_j$

- Propiedad astuta de nuestro Greedy: Siempre asigna trabajo a la máquina con menor asignación. Por lo tanto podemos relacionar al tiempo total $T_i$ con $T_j$
- $T_i - T_j$ era el tiempo $T_k$ para cualquier máquina k. $T_k \geq T_i - T_j$
- Sumando todo los tiempos asignados de las máquinas:
  $$
  \sum_k T_k \geq m(T_i - T_j)
  $$
  $$
  T_i - T_j \leq \frac{1}{m} \sum_k T_k
  $$
  > [!info] Esta es una parte de las cotas del análisis

Por lo tanto:

$$
T_i - t_j \leq T*
$$

- Nos interesa acotar el valor $T_i$ porque nos condiciona nuestra solución T
- Además, tenemos acotado $T_j$, para sacarlo de esta ecuación:
  $$
  T* \geq max_j t_j ==> T_i = (T_i - t_j) + t_j \leq 2T*
  $$
- Por lo tanto, acotamos la solución T a decir que "nunca es peor que el doble del óptimo".

#### Si ordenamos de mayor a menor

##### Demostración: cuánto nos aproximamos

- Si m >= n, Greedy es siempre óptimo
- Si n > m, para estos trabajos en orden, los primeros m+1 trabajos cuestan lo mismo o más que el trabajo m+1. Cualquier solución óptima debe asignar dos de esos trabajos a la misma máquina (demostrable por palomas y nidos)
- Encontramos otra cota de la solución óptima.

  $$
  T* \geq 2t_{m+1}
  $$

- El análisis es análogo: Una de nuestra máquinas en T tuvo más carga que cualquier otra
- Habrá habido un último trabajo $t_j$ en ser colocado en esa máquina
- Ese trabajo debe tener índice mayor o igual a m+1, porque los primeros m trabajos se asignan a máquinas distintas, entonces:$t_{j} \leq t_{m+1}\leq \frac{1}{2}T*$
  ![[Pasted image 20260601160427.png]]

## Problema: Set Cover

Tenemos un Set U de n elementos y un listado S1, S2, ..., Sm de subsets de U.

Un Set Cover es una colección de estos subsets tal que la unión es U.

El uso de cada Subset $S_i$ tiene un costo $w_i$. Queremos minimizar: $\sum_{S_i \in C} w_i$

Para resolver, pensamos en el algoritmo greedy.

Si analizamos Subsets de a uno por vez, nos interesa que el siguiente Subset a agregar a la solución sea aquel que más nos ayuda a acercarnos a la solución

Esto nos da la idea de seleccionar aquel que nos ayude con mayor progreso

Esta medida de progreso debería considerar

- El peso de los subsets
- Los elementos que ese Subset me ayuda a cubrir de U

### Algoritmo greedy

- Empezando por el conjunto de Subsets vacío
- Encontrar que Subset me conviene agregar según la proporción: peso / #elem
- Iterar, recalculando la medida de progreso teniendo únicamente en cuenta aquellos elementos de U que no se han logrado incorporar
- Completar la iteración cuando hayamos cubierto todos los elementos de U

¿Qué tanto peor puede ser el resultado de este algoritmo en comparación a la solución óptima?

Se puede demostrar (K&T 11.3) que el peso obtenido es como mucho O(log n) veces el peso óptimo, para un set U de n cantidad de elementos.

De hecho, es función H(d) (la función armónica) de veces el peso óptimo como mucho, la cual es acotada por O(log n). Siendo d el Subset más grande

Más aún, se ha demostrar que ningún algoritmo de complejidad polinomial puede dar una mejor aproximación... a menos que P = NP

## Problema: Vertex Cover

Dado un grafo, un Vertex Cover es el mínimo Subset de los vértices, tal que se cubran todas las aristas, es decir, que cada arista tenga por lo menos uno de sus bordes en el Vertex Cover.

El uso de cada Vértice $V_i$ tiene un costo $w_i$. Queremos minimizar la suma de los costos.

### Reducción

Empezar pensando un buen problema hacia donde hacer la reducción.

Reducimos a Set Cover

Será posible aprovechar esta solución por Aproximación de Set Cover, para encontrar una solución Aproximada de Vertex Cover?

Set cover encuentra los Subsets a como mucho H(d) veces el óptimo, siendo d el conjunto más grande, que representa en este caso el vértice de mayor grado.

Esto significa que esta aproximación nos da una solución como mucho H(d) veces el óptimo para el Problema de Vertex Cover.

