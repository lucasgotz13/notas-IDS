---
id: 1777586682-programacion-lineal
aliases:
  - Programacion Lineal
tags:
  - tda
---

# Programación Lineal

Es una forma de modelado que nos ayuda a abrir la cabeza.

Nos permite resolver casi todos los problemas que vemos en la materia, formulando de una manera *matemática*

Es una técnica de diseño que permite resolver problemas de optimización de un sistemas de ecuaciones **lineal** en varias variables.

Es decir:
$$
cte_{0}*x_{0} + \dots + cte_{n}*x_{n} \geq cte
$$
Y luego maximizar/minimizar una fórmula en particular (salvo que sólo se quiera una solución válida y nada más).

## Componentes de programación lineal
1. Variables (continuas, enteras, binarias)
2. Ecuaciones e inecuaciones **lineales** que definen restricciones sobre dichas variables:
		$$
		\sum a_{i}x_{i} \geq b
		$$
3. Buscamos maximizar o minimizar una función objetivo: $max \sum c_{i}x_{i}$
4. Luego aplicamos un algoritmo que resuelva el modelo lineal


> [!Warning] Aclaraciones
> Las restricciones van a crear un dominio de soluciones válidas.

En problemas lineales **continuos** la solución óptima siempre va a estar en un vértice

## Ejemplo
Tenemos una empresa TeoAlgoSoft que vende 2 comestibles por kilo: x e y. Por cuestiones normativas (Argentina, no lo entenderías) no podemos vender y en más kilos que el triple de x. Al mismo tiempo, la cantidad de x con el doble de y no puede exceder los 14 kgr. ¿Por qué? Vos seguime el ejemplo. Luego, la cantidad de kilos que exceda x a y no puede ser mayor a 2kgr. La ganancia del día puede verse por $5/kgr del producto x + $3/kgr del producto y.

### Restricciones
- x >= 0
- y >= 0
- y <= 3x --> 0 <= 3x - y
- x + 2y <= 14
- x - y <= 2

### Función objetivo:
$$
max(5x + 3y)
$$

## Ejemplo 2
Nuestra empresa cereales tiene que cumplir con un pedido de al menos 100 kgr del producto estrella de la empresa para el final de la semana, para ser vendido en diferentes supermercados. Para elaborar el producto necesita de amaranto y frutos secos (misma cantidad de cada uno). Para esto contamos con dos proveedores: 
- Valle Patagua: nos vende a $1 el kilo de amaranto (máximo 40kgr)
- Salud Sustentable: nos vende cajas de 2 kgr de amaranto y 5 kgr de frutos secos por $6 (máximo 30 cajas) → vamos a suponer inicialmente que se puede pedir proporción.**

## Variables
- VP: Cuanto compro en Valle Patagua
- SS: Cuanto compro en Salud Sustentable

### Restricciones
- VP <= 40
- SS <= 30
- 5 * SS >= 50
- VP + 2 * SS >= 50

> [!Info] Como necesitamos valores enteros (no podemos comprar 0,5 cajas), las variables tienen que ser **enteras**.


