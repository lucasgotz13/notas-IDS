#algo2

# Iteradores de Hash

Misma idea que iteradores de lista
- Iterador Externo: manualmente Barbara maneja la iteracion
- Iterador Interno: Alan maneja la iteracion, Barbara provee funcion de aplicacion y corte

El iterador va a depender de como este implementado el Hash
El orden con el cual se iteran los elementos es **arbitrario**
## Iterador externo: Primitivas
- `Iterador()`: en Hash que devuelve un iterador externo
- `HaySiguiente()`: Indica si todavia quedan elementos por iterar
- `Siguiente()`: Avanza el iterador para que apunte al siguiente elemento
- `VerActual()`: Devuelve la **clave y el valor** del elemento actual

No hay primitivas para modificar el hash pues no sabemos donde se deberia incluir el nuevo elemento --> Podriamos arruinar la iteracion
### Iterador externo: Iterador()
#### Hash abierto
```
pos actual = 0

mientras no haya lista en pos actual
	pos actual += 1

creo y guardo iter de lista para lista actual

el elemento que busco es el actual del iter de lista
```
#### Hash cerrado (Casi lo mismo que el abierto)

### Iterador externo: HaySiguiente()
Debemos fijarnos que el iterador no este al final del Hash
#### Hash abierto / cerrado
`pos actual es igual al largo de la tabla?`

### Iterador externo: Siguiente()
Debemos avanzar al siguiente elemento, con cuidado si llegamos al final del hash
#### Hash abierto
```
Si no estoy al final del iter de lista
	avanzo el iter de lista
si estoy al final
	mientras no haya lista en pos actual
		pos actual += 1
creo y guardo iter de lista para lista actual
```
#### Hash cerrado
```
pos actual += 1
hasta que no haya OCUPADO en pos actual
	pos actual += 1
el elemento que busco es el que esta en pos actual
```

### Iterador Externo: VerActual()
Devolvemos la clave y el valor asociado del elemento actual
#### Hash abierto
`le pido el actual al iter de lista`
#### Hash cerrado
`Devuelvo lo que haya en pos actual`
### Iterador Externo: casos borde
- Cuando avanzo, tengo que detectar si llegue al final y dejar de intentar avanzarn en ese caso
- Si estoy al final e intento ver el actual, debo fallar
- Si creo un iterador y el Hash esta vacio, el iterador va a estar al final

#### Hash abierto
- Si la posicion en la tabla no tiene elementos hay que elegir entre:
	- No tengo lista (nil)
	- Tengo lista vacia

## Iterador Interno
Misma idea que iterador de listas
- Alan maneja la iteracion
- Primitiva Iterar de Hash
- Recibe una funcion que determina que accion tomar sobre cada elemento, y un booleano que determina si seguir iterando o no.
- La funcion que se pasa por parametro va a recibir la clave y el valor