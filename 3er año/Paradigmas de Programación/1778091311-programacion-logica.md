---
id: 1778091311-programacion-logica
aliases:
  - Programacion Logica
tags:
  - paradigmas
---

# Programación Lógica
- [[#Definiciones|Definiciones]]
- [[#Tipos de datos|Tipos de datos]]
- [[#Cláusulas|Cláusulas]]
- [[#Predicados predefinidos|Predicados predefinidos]]
- [[#Unificación|Unificación]]
- [[#Backtracking|Backtracking]]
- [[#Árbol de búsqueda|Árbol de búsqueda]]
- [[#Depuración en Prolog|Depuración en Prolog]]
- [[#Entrada/Salida básica|Entrada/Salida básica]]
- [[#Predicados de control|Predicados de control]]
- [[#El problema de la negación|El problema de la negación]]
- [[#Aritmética|Aritmética]]
- [[#Listas|Listas]]

Es un paradigma de programación **declarativo** -> Le declaro el problema a resolver.

Se basa en expresar **proposiciones**, **reglas** y **hechos lógicos**, y utilizar un motor de inferencia para resolver problemas.

## Definiciones
- **Proposición**: Una afirmación lógica que puede ser verdadera o falsa.
- **Axioma/Hecho**: Una proposición aceptada como verdadera sin necesidad de prueba.
- **Regla**: Una proposición que define una relación entre hechos y/o otras reglas.
- **Base de datos**: Un conjunto de hechos y reglas que representan el conocimiento en un dominio específico.
- **Objetivo/Consulta**: Una proposición que se desea demostrar o refutar.
- **Estrategia de resolución**: El proceso de buscar una solución a un objetivo utilizando la base de datos.
- **Programa lógico:** Compuesto por una **base de datos** y un **objetivo**. Al ser ejecutado, un **motor de inferencia** se encarga de **probar** o **refutar** el objetivo, utilizando alguna **estrategia de resolución**.

## Tipos de datos
Prolog es **dinámicamente tipado**. Todo valor en Prolog se representa mediante un **término**, que tiene varios subtipos:
- **Términos atómicos**:
	- **Átomos**:  `x`, `azul`, `hola_mundo`, `'Hola, Mundo!'`.
	- **Números**: enteros y de punto flotante. Ejemplos: 42, 3.14.
	- **Variables**: `X`, `Resultado`
		Las variables son **unificadas** con otros términos durante la resolución de objetivos.
		La variables `_` representa una variable anónima y significa "cualquier término".
- **Términos compuestos**:
	- **Estructuras**: Consisten en un átomo (el **functor**) seguido de una lista de argumentos entre paréntesis. Ejemplos: `padre(juan, maria), suma(X, Y, Resultado)`.
		La **aridad** es el número de argumentos que tiene. La notación `f/n` se usa para referirse a un functor `f` con aridad `n`. Por ejemplo: `padre/2`.
		**Azúcar sintáctica**: Algunas estructuras pueden ser escritas como operadores **infijos**. Por ejemplo, para `=/2`: `=(X, Y)` es equivalente a `X = Y`.
	- **Listas**: `[], [1, 2, 3], [X, Y]`
		- Si `T` es una lista, `[H|T]` es una lista con cabeza `H` y cola `T`.
	- **Cadenas**: `"Hola, Mundo!"`.

## Cláusulas
Una base de datos Prolog se compone de un conjunto de cláusulas, que pueden ser **reglas** o **hechos**:
```prolog
q :- p. % regla
h.      % hecho
```

El operador `:-` se lee como <=, de forma que la regla se lee como "p entonces q". El **encabezado** de la regla es q, y el **cuerpo** es p.

Dos o más cláusulas con el mismo functor se consideran parte del mismo **predicado**. Por ejemplo:
```prolog
padre(homero, bart).
padre(homero, lista).
padre(homero, maggie).
```

La **consulta** se escribe como `?- t.` donde t es un término.

## Predicados predefinidos
Disponemos de una gran cantidad de predicados predefinidos, por ejemplo:
`true` / `false` (`fail`): Siempre evalúan a verdadero o falso, respectivamente.
`A, B`: Verdadero si `A` y `B` son ambos verdaderos (and).
`A, B`: Verdadero si `A` o `B` (o ambos) son verdaderos (or).
`X == Y`: Verdadero si `X` e `Y` son términos idénticos.
`X \== Y`: Verdadero si `X` e `Y` no son términos idénticos.
`X = Y`: **Unifica** `X` e `Y` (falso si no son unificables).
`X \= Y`: Verdadero si `X` e `Y` no son unificables.
`var(x)` / `atom(x)` / `number(x)` / ...: Verdadero si `X` es una variable, átomo, número, etc.

## Unificación
Dos términos **unifican** si pueden representar la misma estructura. Si alguno de los términos contiene variables, éstas se **instancian** para lograr la unificación.

Ejemplos:
- padre(homero, bart) unifica con padre(homero, bart).
- padre(homero, bart) no unifica con padre(homero, lista).
- padre(homero, X) unifica con padre(homero, bart) instanciando `X = bart`.
- padre(P, X) unifica con padre(homero, bart) instanciando `P = homero`, `X = bart`.
- 2 + 3 no unifica con 5.

Para **resolver una consulta**, el motor de Prolog:
- Intenta unificar el objetivo con alguna de las cláusulas de la base de datos (buscando de arriba hacia abajo).
- Para las cláusulas de tipo `q :- p`, el objetivo debe unificar con `q`.
- Si la cláusula unificada tiene un cuerpo `p`, se intenta resolver la consulta `?- p.`, con las variables instanciadas en la unificación de `q`.

## Backtracking
Es posible que un objetivo pueda ser unificado con más de una cláusula. En este caso, Prolog sigue una estrategia de búsqueda de tipo **depth-first**: unifica el objetivo con la primera de las alternativas y continúa la búsqueda.

En caso de que alguno de los sub-objetivos falle, se aplica **backtracking**: la búsqueda retrocede, deshace todas las unificaciones hechas, y prueba con la siguiente alternativa.

Notar que el orden de las cláusulas en la base de datos afecta el resultado de la consulta, ya que Prolog intentará unificar las cláusulas en el orden en que aparecen.

## Árbol de búsqueda
Dada una consulta, se puede armar un **árbol de búsqueda** o **árbol SLD** que muestra el proceso de resolución de Prolog.

![[Pasted image 20260506235057.png]]

## Depuración en Prolog
Es posible depurar un programa en Prolog utilizando `trace`.

La ejecución del programa se describe de manera procedimental en términos de cuatro eventos:
- **Call**: Se intenta resolver un objetivo.
- **Exit**: El objetivo se resuelve exitosamente.
- **Fail**: El objetivo no puede ser resuelto.
- **Redo**: Se reintenta resolver un objetivo para encontrar más soluciones. 

## Entrada/Salida básica
`read(X)`: Lee un **término** (terminado con `.`)
 `write(X)`: Escribe el **término** `X` en la salida estándar.
 `nl`: Escribe un salto de línea en la salida estándar.
## Predicados de control
`repeat:` Siempre tiene éxito, y provee un número infinito de soluciones mediante backtracking. Útil para generar bucles. Ejemplo:
```prolog
repeat, write('Ingrese un numero: '), read(X), X == 42.
```

`!`: Proposición de corte. Siempre tiene éxito de inmediato, pero no puede ser resatisfecha a través del backtracking. Por lo tanto, las submetas a su izquierda, en una meta compuesta, tampoco pueden ser resatisfechas mediante backtracking.

`\+`: "No demostrable". Verdadero si el objetivo no puede ser resatisfecho.
```prolog
ilegal(robar).
ilegal(evadir_impuestos).
legal(X) :- \+ ilegal(X).
```

## El problema de la negación
Prolog adopta **el modelo de mundo cerrado: todo lo que no se pueda demostrar como verdadero, es falso**.

De esta manera el predicado `\+` implementa la **negación por falla**:

```prolog
\+ P :- P, !, fail.
\+ _ :- true.
```

Esto puede llevar a resultados inesperados, dado que la negación por falla no es equivalente a la *negación lógica*.

Por ejemplo, dada la regla `legal(X) :- \+ ilegal(X).`, la consulta `?- legal(X)` no puede ser usada para listar todos los valores de `X` que son legales.

## Aritmética
El operador `is` permite escribir predicados que involucran expresiones aritméticas, pero tiene algunas limitaciones -> En su lugar, se recomienda usar la biblioteca `clp(fd)`.

## Listas
Los predicados que involucran listas suelen ser recursivos. Ejemplo:
```prolog
longitud([], 0).
longitud([_|T], L) :- longitud(T, L1), L is L1 + 1.
```

Algunos predicados predefinidos para operar con listas:
- `member(X, L)`: Verdadero si X es un elemento de la lista `L`.
- `append(L1, L2, L3)`: Verdadero si `L3` es la concatenación de `L1` y `L2`
- `reverse(L, R)`: Verdadero si `R` es la lista `L` invertida
- `permutation(L1, L2)`: Verdadero si `L2` es una permutación de `L1`.