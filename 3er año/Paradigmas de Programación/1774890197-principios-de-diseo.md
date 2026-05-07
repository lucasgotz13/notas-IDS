---
id: 1774890197-principios-de-diseo
aliases:
  - Principios de diseño
tags:
  - paradigmas
---

# Principios de diseño

## Algunas definiciones
- *Code smell*: Un indicio de que algo no está bien en el código.
- *Deuda técnica*: Es el costo implícito del trabajo adicional futuro resultante de elegir una solución sobre una más robusta.
- *Refactoring*: Proceso de reestructuración del código para mejorar su legibilidad, mantenibilidad y extensibilidad, sin cambiar su comportamiento externo.

> [!Warning] Advertencia
> Los principios de diseño **no deben convertirse en dogmas** (No se deben aplicar ciegamente)


## Principios

- YAGNI: You Ain't Gonna Need It
	- Solo agregar una funcionalidad si es requerida.
- KISS: Keep It Simple, Stupid!
	- Puede entrar en conflicto con el principio de encapsulamiento (poner los atributos como privados) por ejemplo.
- DRY: Don't Repeat Yourself
- POLA: Principle of Least Astonishment
	- Un componente de un sistema debe comportarse como la mayoría de sus usuarios esperan que se comporte, y no sorprender com comportamientos inesperados.
- KOP: Knuth's Optimization Principle
	- Propone no optimizar el código **prematuramente**.
	- En caso de decidir optimizar **medir el rendimiento** del código antes y después para saber si se debe aplicar la optimización o no.
- SoC: Separation of Concerns
	- **Separación de incumbencias**: Dividir un sistema en partes independientes que abordan diferentes aspectos o dominios relacionados con el problema a resolver.
		![[Pasted image 20260330145232.png]]
- Alta cohesión y Bajo acoplamiento
	- **Cohesión**: Es la medida en que dos elementos de un módulo están relacionados entre sí.
		- Es preferible que los módulos tengan alta cohesión (que sus elementos esten estrechamente relacionados y trabajen juntos para cumplir un propósito específico).
	- **Acoplamiento**: Es la medida en que un módulo depende de otros módulos.
		- Es preferible que los módulos tengan **bajo acoplamiento** (que dependan lo menos posible de otros módulos, lo que facilita su reutilización, mantenimiento y prueba).

## Principios de Diseño (OOP)
- TDA: Tell, don't ask! (cont.)
	- Solicitarle al objeto que lleve a cabo la acción el mismo. (que tenga estado y comportamiento)
- PoLK: Principle of Least Knowledge
	- **Principio del menor conocimiento**: Para promover el bajo acoplamiento, cada módulo debería conocer lo menos posible sobre otros módulos.
	- Aplicado a objetos, un método $f$ de una clase $c$ solo debería invocar métodos de:
		- La propia clase $c$;
		- Los objetos que son atributos de $c$;
		- Los objetos recibidos por $f$ como argumentos;
		- Los objetos instanciados en $f$;
- EDP: Explicit Dependencies Principle
	- Las clases y métodos deben requerir explícitamente los objetos necesarios para funcionar correctamente, en lugar de asumir que están disponibles en el contexto.
		![[Pasted image 20260330153645.png]]

### Principios SOLID
- SRP: Single Responsibility Principle
	- **Principio de responsabilidad única**: Cada clase debe tener una única responsabilidad y propósito.
- OCP: Open/Closed Principle
	- **Principio abierto/cerrado**: Las clases deben estar abiertas para su extensión, pero cerradas para su modificación.
	- Es decir, debe ser posible agregar nuevas funcionalidades a su código existente.
- LSP: Liskov Substitution Principle
	- **Principio de sustitución de Liskov**: Una instancia de una clase debe poder ser sustituida por una instancia de una clase derivada sin "romper" el comportamiento del programa.
- ISP: Interface Segregation Principle
	- **Principio de segregación de interfaces**: Una clase no debe depender de métodos de otras clases que no utiliza.
- DIP: Dependency Inversion Principle
	- **Principio de inversión de dependencias**:
		- Las clases de alto nivel no deben depender de clases de bajo nivel; ambas deben depender de abstracciones.
		- Las abstracciones no deben depender de detalles; los detalles deben depender de las abstracciones.

## Preferir composición sobre herencia
Preferir la composición de objetos en lugar de la herencia para reutilizar código y extender funcionalidades.

![[Pasted image 20260330162250.png]]

## Antipatrones
Un antipatrón es un proceso, estructura o patrón de acción comúnmente utilizado que tiene más consecuencias negativas que positivas.
Ejemplos:
- **God Object**: Una sola clase maneja todo el control en un programa en lugar de distribuirlo entre múltiples clases.
- **Magic Number**: Un valor literal con un significado importante pero no explicado que podría ser reemplazado por una constante con nombre. 
- **Poltergeist**: Objetos efímeros que solo existen para invocar otros métodos en clases.
- **Código spaguetti**: Un sistema de software que carece de una arquitectura perceptible, y su flujo de control es difícil de seguir debido a la falta de estructura