#algo2 
![[Pasted image 20250908194109.png]]

Se tiene un arreglo de N>=3N>=3 elementos en forma de pico, esto es: estrictamente creciente hasta una determinada posición pp, y estrictamente decreciente a partir de ella (con 0<p<N−10<p<N−1). Por ejemplo, en el arreglo `[1, 2, 3, 1, 0, -2]` la posición del pico es p=2p=2. Se pide:

1. Implementar un algoritmo de división y conquista de orden O(log⁡n)O(logn) que encuentre la posición pp del pico: `func PosicionPico(v []int, ini, fin int) int`. La función será invocada inicialmente como: `PosicionPico(v, 0, len(v)-1)`, y tiene como pre-condición que el arreglo tenga forma de pico.
2. Justificar el orden del algoritmo mediante el teorema maestro.

Punto de partida: Partimos a la mitad 

```go
func PosicionPico(v []int, ini, fin int) int {
	if ini == fin {
		return ini	
	}
	
	med := (ini + fin) / 2
	if v[med] > v[med + 1] && v[med] > [med -1] {
		return med		
	} 
	
	if v[med] > v[med + 1] {
		return PosicionPico(v, ini, med)	
	} else {
		return PosicionPico(v, med, fin)
	}
}
```

Complejidad --> Teorema Maestro --> O(log n)

# Búsqueda Lineal vs Ordenar + Búsqueda Binaria

Que me conviene si voy a hacer K búsquedas sobre un vector desordenado?

K * n vs n * log(n) + K * log(n):
- Si k << n (k=1): n * log(n) + 1 * log(n) > 1 * n --> Conviene buscar K veces **lineal**
- Si k = n: n log(n) < n² --> Conviene primero ordenar y después hacer las K busquedas