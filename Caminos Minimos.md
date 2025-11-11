#algo2

# Caminos minimos

## ¿Qué algoritmos para obtener Caminos Minimos conocemos?

-  BFS --> Solo para no dirigidos, no pesados
-  Dijkstra
-  Bellman-Ford

## Complejidades

- BFS: O(V + E)
- Dijkstra: O(V + E log V) 

## Dijkstra

- Diferencia con BFS: Reemplazamos la **cola** por una **cola de prioridad**
- No sirve con pesos negativos