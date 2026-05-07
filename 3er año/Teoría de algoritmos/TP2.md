---
tags:
  - tda
---
Para el algoritmo de programación dinámica, primero tenemos la creación de la matriz de memoria donde se guardaran los datos a medida que avanza el algoritmo. La creación de esta cuesta $O((n+1) * (n+1)) = O(n^2)$, siendo n la cantidad de días de entreno/descanso. Dentro de esta operación, se inicializa el valor de cada celda con un valor constante (0), lo cual tiene un costo amortizado de O(1). Luego, se recorre la matriz para ir llenando cada celda de esta con la información necesaria. La complejidad de las operaciones dentro del recorrido son O(1). Por lo tanto, la complejidad temporal de la función es:
$$
O(n^2) + O(1) + O(n^2) + O(1) = O(n^2)
$$

En cuanto a la complejidad espacial del algoritmo, dado que estamos utilizando una matriz de $(n+1)*(n+1)$ para almacenar los valores de $OPT(i,k)$, esta ocupará un espacio en memoria de $O((n+1)^2) = O(n^2)$

Para la función de reconstruir la solución, se recorre una vez la cantidad de días $n$. Luego, por cada iteración se realizan operaciones las cuales tienen complejidad temporal $O(1)$. Por lo tanto, la complejidad temporal de la función es:
$$
O(n) + O(1) = O(n)
$$
En cuanto a la complejidad espacial del algoritmo de reconstrucción, si bien se utilizan dos arreglos para poder almacenar los días de entreno y los días de descanso, podemos afirmar que la suma de cantidad de elementos entre estos 2 arreglos no va a ser superior a $n$ días. Por lo tanto, la complejidad espacial para este algoritmo es $O(n)$

## Casos de ejecución
### Caso 1: Esfuerzos bajos y altos
Dias: 7
Esfuerzos: [20,2,20,20,2,20,20]
Energías: [10,8,5,4,3,2,1]

La ganancia máxima se encuentra en la primera celda, la cuál es 46

Para hacer la reconstrucción de la solución óptima, debemos hacer lo siguiente por cada día (en relación al algoritmo de reconstrucción previamente mencionado):
![[Pasted image 20260502124626.png]]
- Calculamos la ganancia de entrenar este día  $= min(esfuerzos[dia], energias[energia\_dia])+tabla[dia+1][energia\_dia+1]$
- Luego comparamos este resultado con el valor de la tabla con ese dia y ese k:
	- Si los valores son equivalentes, significa que la ganancia en esa celda de la tabla