---
id: 1776377652-programacion-dinamica-3
aliases:
  - Programacion Dinamica 3
tags:
  - tda
---

# Programacion Dinamica 3: The Return of the King

## Problema de la mochila 2
Tenemos una mochila con una capacidad W. Hay elementos a guardar. Cada elemento tiene un peso que ocupa de la capacidad y un valor. Queremos maximizar el valor de lo que llevamos sin exceder la capacidad.

Supongamos que no es necesario poner "todo un elemento" sino que podemos poner proporciones (fraccionarlos).

> [!INFO] 
> La programación dinámica nos puede ayudar en problemas difíciles que no tengan una solución óptima por Greedy

Vemos el problema en sub-problemas mas pequeños:
- 0 elementos: ganancia = 0
- 1 elemento:
	- El peso del ítem debe ser menor a W, y ocupará ese peso.
	- Si se incluye el ítem tendremos una ganancia acorde a su valor.
- 2 elementos:
	- Existe la posibilidad de incluir o no el 2do ítem en la solución. Consideraciones:
		- Si no se incluye => Solución de tamaño 1.
		- Si se incluye => Tendremos una ganancia acorde a su valor.
		- El ítem debe poder entrar en la mochila, y ocupará ese peso.
- 3 elementos:
	- Con 3 ítems hay que empezar a considerar que los subproblemas mas pequeños deberían poder ayudarme.
	- Este 3er ítem está la posibilidad de incluirlo o no en la solución. Consideraciones.
		- Si no se incluye el ítem, disponemos de la solución de tamaño 2.
		- Si se incluye => Tendremos una ganancia acorde a su valor.
		- El ítem debe poder entrar a la mochila.
		- **Importante**: ¿Cómo sabemos si agregar el 3er ítem es compatible con el segundo o con el primero? ¿O con ambos?				
			![[Drawing 2026-04-16 19.45.15.excalidraw]]

Debemos identificar una fórmula que maximice la ganancia, comparando la posibilidad entre incluir el ítem o no.

### El problema del problema de la mochila
Plantear los sub-problemas como medida de la cantidad de elementos no es suficiente para saber de qué manera la presencia de un elemento condiciona a otros.

### Ecuación de recurrencia
Si $w_i > w$:
$$
OPT(i, w) = OPT(i - 1, w)
$$
Si no:
$$
OPT(i,w) =  max(OPT(i - 1,w), v_{i} + OPT(i - 1, w - w_{i}))
$$

