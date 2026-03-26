---
id: 1773698555-algoritmos-greedy-1
aliases:
  - algoritmos greedy 1
tags:
  - tda
---

# Algoritmos Greedy

## ¿Qué es?

- Aplicamos una regla sencilla que nos permita obtener el/un **óptimo local** a mi **estado actual**.
- Aplicamos iterativamente esa regla, esperando que nos lleve al óptimo general (la mejor solución).

## Cuando tenemos un algoritmo greedy?

Un algoritmo es greedy cuando tenemos dicha regla sencilla que sólo mira el estado actual y que busca un óptimo local. Si no podemos enunciar cuál es el óptimo local, el algoritmo no es greedy o lo estamos planteando mal.

## Ventajas y Desventajas

- No siempre dan el resultado óptimo.
- Demostrar que dan el resultado óptimo puede no ser fácil.
- Son intuitivos de pensar. Son fáciles de entender.
- Suelen funcionar rápido.
- Para problemas complejos pueden ser buenas aproximaciones.

## Ejemplos de algoritmos greedy

- Dijkstra
  - La regla sencilla es que se agarra el vértice que está a menor distancia del origen y que no se haya revisado.
  - El óptimo local al que quiero llegar con esta regla es que una vez el vértice fue visitado entonces se determinó la mayor optimización
- Prim
  - La regla _greedy_ es que la siguiente arista que yo voy a ver es la mas pequeña a la cuál puedo considerar o no (que no genere ciclo).
  - El óptimo local es que el MST hasta cierta iteración agrega un vértice nuevo tal que sea la minima arista.
- Kruskal
  - La regla _greedy_ es que agrego la arista mas pequeña que no me genere ningun ciclo en general
  - El optimo local es similar a Prim.

## Problema de Scheduling

Tengo un aula/sala donde quiero dar charlas. Las charlas tienen horario de inicio y fin. Quiero utilizar el aula para dar la mayor cantidad de charlas.

Óptimo global: Dar la mayor cantidad de charlas.

Óptimo local: Agarrar la charla que finaliza antes (análogo la que empieza ultima). En cada iteración busco poner una charla que ocupe el menor espacio posible.

```python
def scheduling(horarios):
 horarios_ordenados = ordenar_por_horario_fin(horarios)
 charlas = []
 for horario in horarios_ordenados:
  if len(charlas) == 0 or not hay_interseccion(charlas[-1], horario):
   charlas.append(horario)
 return charlas

def hay_interseccion(anterior, nueva):
 return anterior[FIN] > nueva[INICIO]
```

## Árboles de Huffman

Huffman plantea una forma de comprimir un texto en base a la frecuencia de los caracteres en el mismo.

Utiliza un heap (de mínimos) de forma auxiliar para ir generando el árbol de códigos.

Aplicamos a PARALEPIPEDO.

### ¿Por qué es greedy?

Regla: Agarro los 2 caracteres menos frecuentes y los vuelvo mas grandes.

## Problema del Cambio

Se tiene un sistema monetario (ejemplo, el nuestro). Se quiere dar "cambio" de una determinada cantidad de plata. Implementar un algoritmo que devuelva el cambio pedido, usando la mínima cantidad de moneda/billetes.

Si tuvieramos $n$ precio y $c$ cantidad de monedas, la solución cuesta $O(c)$ (no involucra $n$).

¿Y si el sistema monetario fuera [1, 5, 6, 9] y quisiéramos cambio de 11?

¿Por qué falla?
Porque al ser greedy, el algoritmo agarra primero la moneda mas grande, en vez de pensar si la combinacion de otros numeros quizas da mejor.

## Problema de compras con inflación

Tenemos unos productos dados por un arreglo R, donde R[i] nos dice el precio del producto. Cada día debemos comprar uno (y sólo uno) de los productos, pero vivimos en una era de inflación y los precios aumentan todo el tiempo.

El precio del producto $i$ el día $j$ es $R[i]^{j*1}$ ($j$ comenzando en 0).

Implementar un algoritmo greedy que nos indique el precio mínimo al que podemos comprar todo los productos.

Regla: comprar del más caro al más barato.

## Problema de la carga de combustible

Un camión debe viajar desde una ciudad a otra deteniéndose a cargar combustible para poder llegar a destino. El tanque de combustible le permite viajar hasta K kilómetros.

Las estaciones se encuentran distribuidas a lo largo de la ruta siendo d$i$ la distancia desde la estación i-1 a la estación i.

1. Implementar un algoritmo que decida en qué estaciones conviene detenerse a cargar combustible, de manera que se detenga la menor cantidad de veces posible.
2. Indicar y justificar la complejidad del algoritmo.

Regla: que llegue a la mas lejana que pueda.
