---
id: 1773076782-Introduccion
aliases:
  - Introduccion
tags:
  - paradigmas
---

# Introduccion

## Paradigmas de Programación

Es una manera de categorizar los lenguajes de programación según su estilo y enfoque. Entre los paradigmas mas comunes se destacan:

- Imperativos (enfasis en la ejecución de instrucciones)
  - Programación Procedimental (ej. Pascal): Permite agrupar una secuencia de instrucciones en ==procedimientos== (como las subrutinas)
  - Programación Orientada a Objetos (ej. Java, Smalltalk)
  - En este tipo de lenguajes describo **como se resuelve el problema**
- Declarativos (énfasis en la evaluación de expresiones)
  - Programación Funcional (ej. Haskell)
  - Programación Lógica (ej. Prolog)
  - En este tipo de lenguajes describo **cual es el problema que quiero resolver**

Algunos lenguajes son **puros**, es decir, soportan un único paradigma.
Los lenguajes mas utilizados son **multiparadigma**. El programador puede usar el que le sea mas cómodo.
¿Por que existen diferentes paradigmas? => Diferentes problemas se resuelven mejor con diferentes paradigmas.

## Paradigma de Objetos (OOP)

### ¿Que es un objeto?

Es una entidad (habitualmente almacenada en memoria) que tiene **identidad**, **estado** y **comportamiento**

Un sistema orientado a objetos se forma de un conjunto de objetos que interactuan pasando mensajes entre si.

### Estilos de OOP

Una característica importante en los lenguajes orientados a objetos es la posibilidad de definir objetos con comportamiento similar. Existen dos variantes:
- Basado en **clases**: Todo objeto es una **instancia** de una **clase** específica.
- Basado en **Prototipos**: Todo objeto está asociado a otro (su **prototipo** o **padre**).

## Java

Características:
- De propósito general.
- Multiparadigma, principalmente OOP.
- Basado en clases.
- Recolector de basura automático.
- Tipado estático y fuerte.
- Compilación a bytecode y ejecución en una máquina virtual (JVM).
	- Portabilidad: "Write once, run anywhere"
	- Windows, Linux, MacOS, Android, etc.

Se distribuye en dos paquetes:
- JDK: *Java Development Kit*. Incluye herramientas de desarrollo y la JVM
- JRE: Java Runtime Environment. Incluye la JVM y las bibliotecas estándar.

### Definiciones

**Clase**: Plantilla para crear objetos. Define los aspectos que comparten todos los objetos creados a partir de la clase (**atributos** y **métodos**).

**Instancia**: Un objeto creado a partir de una clase. Cada instancia tiene su propia **identidad**, que permite distinguirla de otras instancias. Al crearse una instancia se reserva memoria para almacenar su **estado**.

**Atributos**: Variables de instancia que almacenan el **estado** de un objeto. Alias: **miembros**, **campos**.

**Métodos**: Funciones que operan sobre un objeto. El conjunto de métodos definidos por una clase determinan el **comportamiento** del objeto. La forma de enviar un **mensaje** a un objeto es invocar uno de sus métodos.

**Constructor**: Método especial que es invocado automáticamente cuando se crea una instancia de la clase.

### Generalidades

- El código se organiza en **paquetes** (carpetas) y **clases** (usualmente un archivo `.java` por cada clase).
- Guía de estilo
	- Clases: PascalCase
	- Variables, atributos y métodos: camelCase
	- Constantes: UPPER_CASE
- Crear una instancia de una clase: `new Clase(...)`
- Acceder a un atributo, invocar un método: `instancia.atributo`, `instancia.metodo(...)`
- En un objeto mutable, es recomendable calificar sus atributos como `private`, para evitar que puedan ser manipulados desde fuera de la clase, y opcionalmente definir **métodos de acceso** (*getters* y *setters*) públicos.
- El modificador `final` indica que una variable o atributo es inmutable.
- El modificador `static` indica que un atributo o método pertenece a la clase en sí, y no a una instancia específica.

## UML

*Unified Modeling Language*: Proporciona una forma estándar de visualizar el diseño de un sistema.
### Diagrama de clases

![[Pasted image 20260309162728.png]]
Estos diagramas nos permiten visualizar rápidamente como es el diseño del sistema sin tener que analizar el código.

#### ¿Cómo se lee?
- Cada clase se dibuja en un recuadro rectangular.
- Se pone el nombre de la clase como encabezado.
- Se pone primeros los atributos y luego los métodos.
- Si un atributo es de tipo objeto (como se ve en el diagrama con "juego"), se pone una flecha indicando de donde viene ese tipo. 
- Luego, la clase Juego depende de la clase Resultado.
### Relaciones entre clases

![[Pasted image 20260309163444.png]]
### Diagrama de secuencia

![[Pasted image 20260309164647.png]]
Muestra los actores del sistema, una linea de tiempo, los mensajes que se van mandando unos objetos a otros.