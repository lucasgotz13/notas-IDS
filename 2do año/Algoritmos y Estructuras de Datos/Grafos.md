#algo2 

# Grafos

Se componen de
- V: Cantidad de vértices
- E: Cantidad de aristas

## Tipos de grafos
- Grafos dirigidos: Las aristas tienen una dirección asociada (Vértice de origen y vértice de destino)
- Grafos no dirigidos: Es una relación **bidireccional** (No hay origen o fin)
- Con peso: Tienen un valor asociado
- Sin peso: No tienen ninguno

## Listas de adyacencia
### Diccionario de Diccionario
```javascript
{
A: {B: "", D: ""},
B: {C: ""},
C: {},
D: {}
}
```


|                   | Memoria  |    Agregar vértice     | Agregar arista | Ver si A --> B | Sacar vértice | Sacar arista |
| :---------------: | :------: | :--------------------: | :------------: | :------------: | :-----------: | :----------: |
| Matriz incidencia | O(V X E) |          O(E)          |      O(V)      |      O(E)      |   O(V x E)    |   O(V x E)   |
| Matriz adyacencia |  O(V²)   |      O(V) (redim)      |      O(1)      |      O(1)      |     O(1)      |     O(1)     |
| Lista adyacencia  | O(V + E) | - OLL (V)<br>- ODL (1) |      O(V)      |      O(V)      |   O(V + E)    |     O(V)     |
| LA: dict de dict  |  O(V+E)  |          O(1)          |      O(1)      |      O(1)      |     O(V)      |     O(1)     |

*OLL: Lista de lista*
*ODL: Diccionario de lista*
