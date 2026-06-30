En el presente trabajo práctico nos centraremos en el desarrollo y análisis de un algoritmo de Backtracking para resolver un problema NP-Completo, como también el análisis de posibles aproximaciones.

## ¿Qué es un algoritmo de Backtracking?
Un algoritmo de Backtracking es una técnica de diseño de algoritmos en la cuál se realiza una búsqueda exhaustiva por el espacio de soluciones del problema, construyendo soluciones candidatas de forma incremental. En cada paso, el algoritmo extiende la solución parcial añadiendo un nuevo elemento. Si en algún momento la solución parcial no cumple con las restricciones, o no conduce a una solución válida o mejor que la actual, se poda esa rama y retrocedemos al estado anterior para explorar alternativas. 

## ¿Qué es la Programación Lineal?
Es una técnica de diseño (matemática) que permite resolver problemas de optimización de un sistema de ecuaciones lineal en varias variables y luego maximizar o minimizar una fórmula en particular.

## ¿Qué es un algoritmo de aproximación?
Son algoritmos diseñados para correr en tiempo polinomial, y que brindan soluciones que garantizan estar cerca de la solución óptima (y que también es demostrable). Generalmente son utilizados para resolver problemas NP-difícil, donde encontrar una solución óptima en tiempo polinomial resulta ser un objetivo inalcanzable.

## Descripción del problema
Dado un conjunto $A$ de $n$ elementos y $m$ subconjuntos $B_1,B_{2},...,B_{m}$​​ de $A$ ($Bi⊆A∀i$) , queremos el subconjunto $C⊆A$ de menor tamaño tal que $C$ tenga al menos un elemento de cada $B_{i}$​ (es decir, $C∩B_{i}≠∅$). En nuestro caso, $A$ son los jugadores convocados, los $Bi$​ son los deseos de la prensa, y $C$ es el conjunto de jugadores que deberían jugar contra Burkina Faso si o si

## Objetivo
Determinar