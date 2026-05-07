#algo2 
# Iteradores Externos

## Beneficios

- Abstraerme de cómo está implementado el TDA
- Tener una forma genérica de acceder al TDA
- Si el TDA cambia internamente, el usaurio que usa el iterador no se entera
- Puede llegar a tener lógica más compleja

```go
iter := lista.Iterador()
for iter.HaySiguiente() {
	dato = iter.VerActual()
	hacer_algo(dato)
	iter.Siguiente()
}
```

# Iteradores Internos

Realiza la iteración de forma transparente al usuario, el usuario no maneja directamente un iterador ni administra su memoria

## Diferencias con el externo
- No se puede crear un iterador interno
- No se puede manejar paso a paso un iterador

## Cómo se usan?

```go
// Función que provee Alan.
func (tda TDAImpl[T]) Iterar(visitar func(t) bool)

// función que provee Bárbara
func (v int) bool
```
### Del lado de Alan
```go
func (tda TDA[T]) Iterar(visitar func(t) bool) {
	// Recorrer toda la lista usando un for (for lista.primero != nil)
}
```
### Del lado de Bárbara
#### Ej 1
```go
lista.Iterar(func(v int) bool) {
	fmt.Println(v)
	return true
}
```
#### Ej 2
```go
contador := 0
lista.Iterar(func(v int) bool) {
	contador += v
	return true
}
```
#### Ej 3
```go
contador := 0
lista.Iterar(func(v int) bool) {
	contador += 1
	fmt.Println(v)
	return contador < 5 // Cuando esto es false, para el iterador
}
```

