---
id: 1779914281-reducciones-y-clases-de-complejidad
aliases:
  - Reducciones y Clases de Complejidad
tags:
  - tda
---

# Reducciones y Clases de Complejidad

Los problemas que venimos viendo se pueden categorizar en términos de dificultad (en base a su complejidad).

Vamos a empezar a hablar de problemas "fáciles" y "difíciles".

Supongamos que en un recuperatorio de un parcial presentan un ejercicio Y, el cuál se resuelve de manera similar al ejercicio X del parcial el cuál estamos recuperando.

¿Qué comparación podríamos establecer entre el ejercicio X y el ejercicio Y?

Yo pude usar la solución del ejercicio X para resolver el Y => El ejercicio Y no puede ser mas difícil que el ejercicio X => **X resultó igualmente o más difícil que Y**.

Y, entonces, se pudo **reducir** a resolver X.

## ¿Qué es una reducción?

Es una herramienta para comparar la dificultad entre problemas.

> [!Info] Formalmente
> Una instancia arbitraria del problema Y, ¿puede ser resuelta por una cantidad de pasos polinómicos y una cantidad de llamados polinómicos a la caja que resuelve X?
> Si es así, entonces se dice que "Y es reducible polinomialmente a X".
>
> $$
> Y \leq_p X
> $$

## ¿Para qué sirve?

Como Y es a lo sumo tan díficil como X, si X se puede resolver en tiempo polinomial, entonces Y **también puede resolverse en tiempo polinomial**.

## Ejemplos

### 1. Ordenar vs Encontrar el máximo

¿Se puede reducir el problema de _Encontrar el máximo de un arreglo_ al problema de _ordenar_.

Si no sabemos encontrar el máximo, ese gran problema se reduce a ordenar y ver una posición.

Entonces: Ordenar es _al menos_ tan difícil como encontrar el máximo en un arreglo.

Reduzco la posible complejidad del problema a que **lo sumo** es tan difícil como otro problema.

Sabemos que hay un algoritmo polinomial para ordenar => Encontrar el máximo también se puede resolver en tiempo polinomial.

### 2. Bipartite Matching

Este problema lo resolvimos con una reducción! => [[1778191360-redes-de-flujo-y-algoritmo-de-ford-fulkerson#Aplicación II Perfect Bipartite Matching|Perfect Bipartite Matching]]

### 3. Problema del caballo y camino hamiltoniano

Reducimos el problema del caballo a camino hamiltoniano

### 4. Independent Set y N-Reinas

Pudimos ver que el problema de N-Reinas se puede reducir a Independent Set.

### 5. Subset Sum y Problema de la mochila

Subset Sum se puede reducir al problema de la mochila => Subset Sum es a lo sumo tan difícil como el problema de la mochila o el problema de la mochila es tan difícil como Subset Sum.

> [!NOTE]
> Los problemas que se reducen ida y vuelta significan que tienen la misma dificultad (o que son lo mismo)

### 6. Búsquedas I

¿Podemos reducir polinomialmente el problema de "Buscar un elemento en un arreglo ordenado" a "Buscar un elemento en un arreglo desordenado"? => Si

¿Podemos al revés? => Si
Mi paso polinomial es ordenar el arreglo. Luego puedo usar la solución del otro problema.

#### 6b. Búsquedas II

¿Podemos reducir polinomialmente la búsqueda del máximo de un arreglo a la búsqueda de un _elemento_ en un _arreglo_?

No se puede hacer polinomialmente porque no sabemos el número que tenemos que buscar.

> [!NOTE]
> Problemas de decisión:
> A partir de ahora vamos a plantear los problemas de una forma _más booleana/binaria_. Por ejemplo, en Independent Set el problema original (de optimización) es encontrar el set independiente más grande, pero vamos a plantear _si existe un set de (al menos) tamaño k._

### 7. Independent Set y Vertex Cover

Sabemos que no podemos resolver ambos en tiempo polinomial, pero ¿y su dificultad relativa?

Teorema: S es un set independiente de G sii $V - S$ es vertex cover de G.

Demostración:
Si tengo un IS S, si agarro una arista cualquiera (v, w), no pueden estar ambos vértices en S, entonces necesariamente al menos uno de ellos tiene que estar en $V-S$ => pasa para todas las aristas => $V-S$ es VC

Suponemos un VC (V-S), y agarramos un par de vértices cualesquiera en S. Supongo que están unidos por una arista (suponer que no es IS), pero entonces habría una arista no cubierta por V-S => Mi suposición genera el absurdo.

#### Reducimos usando teorema

Reducimos: IS <= VC => Si tenemos una caja negra que resuelve si un grafo tiene un VC de tamaño a lo sumo $k$, para ver si tiene un IS de tamaño $X$, le consultamos a la caja negra asi el mismo grafo tiene un VC de tamaño a lo sumo $k = n - X$.

Hacemos similar al revés.

Como $IS \leq_p VC$ y $VC \leq_p IS$, son igual de difíciles.

#### ¿Para qué sirve?

> [!DANGER] IMPORTANTE
> Si sabemos que Y "no se puede" resolver en tiempo polinomial, entonces X tampoco.

## SAT y 3-SAT

### Demostración que son equivalentes

3-SAT $\leq_p$ SAT => Trivial

SAT $\leq_p$ 3-SAT:

- Cláusulas con 2 términos (w, y): reemplazar por ($y \vee   w \vee  z$) y ($y \vee   w \vee  \bar{z}$)
- Cláusulas con 1 término (y): Reemplazamos esa cláusula por ($y \vee z_{1} \vee z_{2}$) y demás variantes (4)
- Cláusulas con 3 términos: nada que hacer
- Cláusulas con más de 3:
  ![[Pasted image 20260528125427.png]]

### ¿Se puede reducir el problema de 3-SAT a Independent Set?

1. Ponemos nodos = términos ($3k$ nodos) de cada cláusula
2. Creamos triángulos por cada cláusula
3. Ponemos aristas en posibles conflictos (variables opuestas).
4. Se puede demostrar que G tiene un IS de tamaño $k$ $\iff$ el 3-SAT es satisfacible.

Si Hay 3-SAT, hay Independent Set:

- Si es satisfacible, al menos 1 nodo de cad triángulo es True/1. Agarramos un vértice de cada triángulo tal que valga True/1 => Ese set es independiente (no puede generar conflictos).

Si hay Independent Set, hay 3-SAT:

- Por cada $x_i$, si está en el set, va 1, si está el complemento va el 0, si no hay ninguno, ponemos alguno en 0 y otro en 1 (no pueden estar ambos). Como hay es un independent set **de tamaño k** => necesariamente hay al menos un 1 por cada triángulo => se cumple 3-SAT.

> [!TODO] Ver el ejercicio en el video (se ve mejor)

## Problemas vs Algoritmos vs Chequeos

Un problema puede tener diferentes soluciones => tomamos lo más eficiente.

Dado un problema un Algoritmo nos da una solución.

Dado un problema y una solución, deberíamos poder también tener un _validador_.

Decimos que tenemos un _cetificador/validador eficiente_, si dicho validador es correcto y ejecuta en tiempo polinomial.

## Clases de Complejidad

P: Problemas que se pueden resolver en tiempo polinomial (de _forma eficiente_)

NP: Problemas para los que existe un _cetificador eficiente_ => se pueden validar en tiempo polinomial.

Todo problema que está en P, está en NP.

No se sabe todavía si todo problema que está en NP se puede resolver en P (tiempo polinomial). => **Problema del milenio**
