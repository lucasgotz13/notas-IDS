---
id: 1778178854-programacion-lineal-ii
aliases:
  - Programacion Lineal II
tags:
  - tda
---

# Programación Lineal II

## Independent Set
Planteamos variables binarias

$Yi$: el vértice $i$ es parte del independent set
$R = \sum_{i}Yi$. Queremos max(R)

$\forall (i, k) \in E, Y_{i} + Y_{k} \leq 1$

Queremos tener restricciones respecto a la cantidad de vértices, **no a la cantidad de aristas**.

Tengo que hacer que la restricción deje de restringir => **Truco de Big-M**

Entonces:
$$
\forall i, Y_{i} + \sum_{k\in adyacentes(i)} Y_{k} \leq 1 + M(1 - Y_{i})
$$
Si $Y_{i}$ vale 1, M va a ser 0. 
$M = |V| + 1$

## Problema del cambio
$v_{i}$: valor de la moneda de denomianción i (constante)
C: Cambio al que queremos llegar (constante)
$M_{i}$: Cantidad de monedas de denominación i que usamos para el cambio.
$$
\sum_{i}v_{i}\times M_{i} = C, \space min\sum_{i}M_{i}
$$

## Problema del coloreo
$X_{pais, color }$

$\forall pais:\sum_{c}X_{pais,c} = 1$

$$
\forall E(p_{1},p_{2}) \in G:\forall c:X_{p_{1},c} + X_{p_{2},c} \leq 1
$$

Así, tenemos países * colores * adyacencias cantidad de inecuaciones, queremos reducir a tener países * colores al menos.

Para reducir la cantidad de restricciones, podemos plantear usar *Big-M*

$$
X_{p_{i},c} + \sum_{p_{j}\in ady(p_{i})}X_{p_{j},c} \leq 1 + M(1 - X_{p_{i}},c)
$$

> [!Todo] Hacer ejercicio del clique


## Problema del viajante
1. Agregamos virtualmente las aristas faltantes con peso F = "infinito" (= sumatoria de todas las aristas existentes + 1).
2. Vamos a construir nuestras variables $Y_{i,j} = 1$ si usamos la arista i -> j (0 sino).
3. $\sum_{j}Y_{i,j} = 1$ => de todos salgo; $\sum_{i}Y_{i,j} = 1$ => a todos entro.
4. Evidentemente queremos minimizar $\sum _{i}\sum_{j}$ peso(i,j) $Y_{i,j}$
Esto sólo no sirve, porque si bien encuentra ciclos **no estan si o si conectados** => Necesitamos un solo ciclo

### Agregamos mas restricciones
$p_{i}$: número de secuencia en la cual visito a la ciudad i
$$
p_{i} - p_{j} + nY_{i,j} \leq n-1
$$

## Problema del tp1
Vamos haciéndonos preguntas:
1. ¿Cómo hacemos que cada equipo quede en un "slot"/orden determinado?
   $Y_{i,j}$: El equipo i se analiza en el orden j.
   $$
   \sum_{i}Y_{i,j} = 1\forall j \space \sum_{j}Y_{i,j} = 1\forall i
   $$
   
2. Una vez obtenido el orden, necesitamos obtener el momento en el que termina de analizarse cada equipo i -> Necesitamos considerar quiénes se analizaron antes!
   Primero, definamos una variable nueva que tenga el valor del orden de cada equipo.
   $$
   p_{i} = \sum_{j}j \cdot Y_{i,j}\space\forall i
   $$
3. Una vez que sé quiénes se analizaron antes -> ¿cuándo termina de analizarse el equipo i?
4. Modelado cuándo termina cada equipo, ¿qué tenemos que hacer?

## Los algoritmos por detrás
### Método Simplex
Al ser un problema lineal, los óptimos van a estar sí o sí en vértices.

El algoritmo es en sí greedy: busca óptimos locales esperando que sean el óptimo general también.

Complejidad: O(Cantidad de vértices) <= $O(2^n)$

Caso lineal continuo: se demostró que es $O(n^9)$

#### Ejemplo
$X_{1} + X_{2} \leq 5$
$X_{1} + 4X_{2} \leq 10$
$Z_{max} = \frac{1}{2}X_{1} + X_{2}$

Tengo que transformar mis menores iguales en iguales

1. Pasamos a igualdades agregando variables de Slack
   $X_{1} + X_{2} + S_{1} = 5$
   $X_{1} + 4X_{2} + S_{2} = 10$   
   Luego lo que haríamos es ir despejando variables para ir obteniendo vértices, paso a paso.
   Ejemplo: el (0,0)

#### Ejemplo mas completo

$2X_{1} + 2X_{2} \leq 600$
$4X_{2} \leq 600$
$2X_{1} + 4X_{2} \leq 800$
$Z_{max} = 8X_{1} + 10X_{2}$

Usando variables de Slack:

$2X_{1} + 2X_{2} + S_{1} = 600$
$4X_{2} + S_{2} = 600$
$2X_{1} + 4X_{2} + S_{3} = 800$
$Z_{max} = 8X_{1} + 10X_{2} + 0S_{1} + 0S_{2} + 0S_{3}$

![[Pasted image 20260507173008.png]]

![[Pasted image 20260507172949.png]]

Luego, vamos a buscar una solución válida, y luego movernos viendo el gradiente.

Inicialmente comenzamos considerando las slacks (Vértice nulo), y vamos "incorporando variables".

![[Pasted image 20260507173439.png]]

Incorporamos $X_{1}$

![[Pasted image 20260507173942.png]]

### Branch and Bounds
Es esencialmente backtracking, aplicando branching para ver diferentes alternativas, con bounds (restricciones) como podas.

Pasos:
1. Buscamos solución relajada (no consideramos variables enteras)
2. Sobre la solución relajada, para variables enteras, vemos una variable y volvemos a resolver agregando una restricción: $X <= [a]$ , y otra vez con $X \geq [a]+ 1$, y además vemos que valga eso. Ramificamos y resolvemos.
3. Seguir aplicando 2 hasta que todas las variables que deban ser enteras sean enteras. Vamos quedándonos con la mejor solución cada vez que volvemos.