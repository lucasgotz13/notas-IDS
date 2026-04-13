---
id: 1775772936-programacion-dinamica-1
aliases:
  - Programacion Dinamica 1
tags:
  - tda
---

# Programación Dinámica 1

- [[#Fibonacci|Fibonacci]]
	- [[#Fibonacci#Definición recursiva:|Definición recursiva:]]
	- [[#Fibonacci#Programación Dinámica|Programación Dinámica]]
		- [[#Programación Dinámica#Fibonacci iterativo|Fibonacci iterativo]]
- [[#Memoization o Memorización|Memoization o Memorización]]
	- [[#Memoization o Memorización#¿Por qué preferimos la forma iterativa (bottom up) a la recursiva (top down)?|¿Por qué preferimos la forma iterativa (bottom up) a la recursiva (top down)?]]
- [[#Solución por Programación Dinámica|Solución por Programación Dinámica]]
- [[#Problema de Scheduling con pesos|Problema de Scheduling con pesos]]
	- [[#Problema de Scheduling con pesos#Cosas que sabemos hasta ahora|Cosas que sabemos hasta ahora]]
	- [[#Problema de Scheduling con pesos#Complejidad|Complejidad]]
- [[#Recapitulación|Recapitulación]]
- [[#¿Cómo podemos saber que podremos utilizar PD?|¿Cómo podemos saber que podremos utilizar PD?]]

## Fibonacci

Vamos a usar este problema como base de como hacer programación dinámica y vamos a poder volver a este problema a hacer analogías en caso de necesitarlo para otro problema.

### Definición recursiva:
Casos base: f(0) = 0, f(1) = 1
Caso general: f(n) = f(n-1) + f(n-2)

```python
def fib(n):
	if n == 0:
		return 0
	if n == 1:
		return 1
	return fib(n-1) + fib(n-2)
```

Arbol de llamadas recursivas:
![[Pasted image 20260409192919.png]]
=> Estamos repitiendo cálculos ya hechos. => Complejidad: $O(2^n)$

### Programación Dinámica

Cuando la resolución combinatoria puede implicar repetir cálculos, PD nos va a ayudar a evitar los recálculos aprovechando lo ya hecho.

```python
def fib_memorioso(n):
	M_FIB = [None] * (n+1)
	return fib_rec_memorioso(n, M_FIB)

def fib_rec_memorioso(n, M_FIB):
	if n == 0:
		return 0
	if n == 1:
		return 1
	if M_FIB[n-1] == None:
		M_FIB[n-1] = fib_rec_memorioso(n-1, M_FIB)
	if M_FIB[n-2] == None:
		M_FIB[n-2] = fib_rec_memorioso(n-2, M_FIB)
	
	M_FIB[n] = M_FIB[n-1]+ M_FIB[n-2]
	return M_FIB[n]
```

#### Fibonacci iterativo
```python
def fib_iterativo(n):
	M_FIB = [NONE] * (n+1)
	M_FIB[0] = 0
	M_FIB[1] = 1
	for i in range(2, n+1):
		M_FIB[i] = M_FIB[i-1] + M_FIB[i-2]
	return M_FIB[n]
```

**Complejidad**: $O(n)$

A nivel de memoria, esto sigue siendo mejorable => Para calcular el valor $n$ necesitamos solo los valores $n-1$ y $n-2$.

```python
def fib_dinamico(n):
	if n == 0:
		return 0
	if n == 1:
		return 1
		
	anterior = 0
	actual = 1
	
	for i in range(1, n+1):
		nuevo = actual + anterior
		anterior = actual
		actual = nuevo
	return actual
```

## Memoization o Memorización

> [!Info] La técnica de guardar los resultados previamente calculados se llama Memoization

- Nos permite pasar de un tiempo de ejecución exponencial a uno polinomial

### ¿Por qué preferimos la forma iterativa (bottom up) a la recursiva (top down)?

1. Es mucho más fácil de entender qué pasa cuándo.
2. Como consecuencia de lo anterior, **mucho** más fácil calcular la complejidad.
3. Este tipo de resoluciones suelen ser más fáciles de resolver de forma inductiva que recursiva.
4. Es más fácil cometer errores en la versión recursiva.
5. Nos estructura mucho más cómo pensar la solución => Primero la ecuación de recurrencia, después programar.
6. Se pueden aplicar optimizaciones de memoria fácilmente.

## Solución por Programación Dinámica
- Se basa en la idea de Memoization
- Construye iterativamente las soluciones a los subproblemas hasta llegar a la solución del problema original.
- Se consigue la solución al problema gracias a que tenemos una forma de construir la solución a problemas más grandes en función de problemas más pequeños.
- Establecemos una lógica inductiva: "Si yo puedo asumir que ya tengo calculados todas las soluciones anteriores, ¿cómo puedo usarlos para construir la que necesito?"

## Problema de Scheduling con pesos
Tengo un aula donde quiero dar charlas. Tienen horario de inicio/fin **y un peso asociado al valor de cada charla**.
Quiero utilizar el aula para **maximizar la sumatoria de pesos de las charlas dadas**.

El algoritmo greedy para el problema original no nos sirve.

### Cosas que sabemos hasta ahora

![[Pasted image 20260409203129.png]]

- Nos quedamos con la suposición de que sabemos las soluciones de problemas más pequeños, **llamémosle OPT**.
- La última charla en particular puede o no pertenecer a la solución
- Si no damos esa charla, entonces el problema más pequeño puede excluir esta charla
- Si damos esa charla, entonces el problema más pequeño debe excluir todas las charlas que terminen después del comienzo de esta charla
- De estas dos opciones deberíamos siempre seleccionar aquella que maximice la sumatoria de los pesos
$$
OPT(j) = max(v_{j} + OPT(p(j)), OPT(j-1))
$$
Esta es nuestra ecuación de recurrencia => Programamos a partir de haber encontrado esto.

![[Pasted image 20260409205158.png]]
### Complejidad
Ordenar por tiempo de fin: $O(n \log n)$
Obtener p[i]: $O(\log n)$ => obtener p: $O(n \log n)$
El cálculo de M_SCHE: $O(n)$

Total: $O(n \log n)$

## Recapitulación
- Exploración implícita del espacio de posibles soluciones.
- Descomposición del problema en subproblemas que permitan construir las soluciones de problemas más grandes.
- Nos basamos en la intuición que nos da la Memorización para reconocer los sub-problemas y utilizarlos para construir la solución.
- Una vez que tenemos todas las soluciones memorizadas, el problema está resuelto.
- Nos ayuda evitando explorar un espacio exponencial de soluciones por fuerza bruta.
- De esa manera podemos reducir la complejidad temporal de nuestro algoritmo significativamente.

## ¿Cómo podemos saber que podremos utilizar PD?
1. Hay un número polinomial de subproblemas.
2. La solución al problema original puede ser construido a partir de soluciones a subproblemas.
3. Hay un orden natural de los subproblemas de menor a mayor. Los subproblemas "mayores" son resueltos mediante la composición de problemas "menores".