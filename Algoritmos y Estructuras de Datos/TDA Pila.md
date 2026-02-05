# TODO LIST

- [x] Se pueda crear una Pila vacía, y ésta se comporta como tal.
- [x] Se puedan apilar elementos, que al desapilarlos se mantenga el invariante de pila (que esta es LIFO). Probar con elementos diferentes, y ver que salgan en el orden deseado.
- [ ] _Prueba de volumen_: Se pueden apilar muchos elementos (1.000, 10.000 elementos, o el volumen que corresponda): hacer crecer la pila, y desapilar elementos hasta que esté vacía, comprobando que siempre cumpla el invariante. Recordar _no apilar siempre lo mismo_, validar que se cumpla siempre que el tope de la pila sea el correcto paso a paso, y que el nuevo tope después de cada `desapilar` también sea el correcto.
- [x] Condición de borde: comprobar que una pila vacía se comporte como recién creada.
- [x] Condición de borde: las acciones para desapilar y ver tope de una pila recién creada son inválidas.
- [x] Condición de borde: la acción para ver si una pila recién creada está vacía es verdadero.
- [x] Condición de borde: las acciones para desapilar y ver el tope de una pila a la que se le apiló y desapiló hasta estar vacía son inválidas.
- [x] Probar apilar diferentes tipos de datos: probar con una pila de enteros, con una pila de cadenas, etc…