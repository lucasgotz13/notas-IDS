---
id: 1773681613-abstraccion-encapsulamiento-herencia-y-polimorfismo
aliases:
  - Abstraccion, encapsulamiento, herencia y polimorfismo
tags:
  - paradigmas
---

# Abstracción, encapsulamiento, herencia y polimorfismo

- [[#Abstracción|Abstracción]]
	- [[#Abstracción#Interfaces|Interfaces]]
	- [[#Abstracción#Composición y agregación|Composición y agregación]]
- [[#Encapsulamiento|Encapsulamiento]]
	- [[#Encapsulamiento#Getters y Setters|Getters y Setters]]
- [[#Polimorfismo|Polimorfismo]]
	- [[#Polimorfismo#Polimorfismo por sobrecarga|Polimorfismo por sobrecarga]]
	- [[#Polimorfismo#Polimorfismo por coerción|Polimorfismo por coerción]]
	- [[#Polimorfismo#Polimorfismo paramétrico (*generics*)|Polimorfismo paramétrico (generics)]]
	- [[#Polimorfismo#Polimorfismo por inclusión o de subtipos|Polimorfismo por inclusión o de subtipos]]
- [[#Herencia|Herencia]]
	- [[#Herencia#La herencia y las jerarquías de clases|La herencia y las jerarquías de clases]]
	- [[#Herencia#Redefinición de métodos|Redefinición de métodos]]
	- [[#Herencia#La clase Object|La clase Object]]
	- [[#Herencia#Java: herencia y constructores|Java: herencia y constructores]]
	- [[#Herencia#Clases abstractas|Clases abstractas]]
	- [[#Herencia#Limitación de la herencia múltiple|Limitación de la herencia múltiple]]
	- [[#Herencia#Limitación de la herencia simple|Limitación de la herencia simple]]

## Abstracción

> [!info]- Definición
> Proceso cognitivo en el que se seleccionan las características más relevantes de un sistema, y se **omiten los detalles no importantes.**

Es la creación de un **modelo simplificado** para representar un **sistema complejo**, concentrándose únicamente en los conceptos relevantes para un **dominio particular**.
En el paradigma procedimental, la abstracción se logra mediante **funciones** y **procedimientos**.

### Interfaces

En el paradigma de objetos, una manera de abstraer objetos es mediante la definición de **interfaces**

```java
public interface Lista {
 void agregar(Object element);
 Object obtener(int index);
 int cantidad();
}

public void armarListaSupermercado(Lista lista) {
 lista.agregar("café");
 lista.agregar("azúcar");
 lista.agregar("palmitos");
}
```

### Composición y agregación

Otra forma de lograr la abstracción es mediante la **composición** y **agregación de objetos**.

```java
public class VectorDinamico implements Lista {
 // Detalles de bajo nivel de abstracción
 private Object[] elementos;
 private int cantidad;
 public VectorDinamico() { ... }
 public int capacidad() { ... }
 public void extender(...) { ... }
 // Implementación de la interfaz:
 @Override public void agregar(Object element) { ... }
 @Override public Object obtener(int index) { ... }
 @Override public int cantidad() { ... } }
```

## Encapsulamiento

> [!info]- Definición
> El término **encapsulamiento** tiene dos significados:
>
> - La **agrupación de estado y comportamiento** en una unidad conceptual (la clase).
> - La aplicación de **mecanismos de restricción de acceso** a los atributos y métodos, para **ocultar los detalles internos de un objeto** (con el objetivo de que queden **inaccesibles**, además de ocultos)

En Java la restricción de acceso se logra mediante el uso de **modificadores de acceso**: `private`, `protected` y `public`

### Getters y Setters

Una práctica común es definir **métodos de acceso** (_getters_) y **métodos de modificación** (_setters_) para acceder y modificar los atributos de una clase.
Los setters permiten entre otras cosas validar que no se violen las **invariantes** del objeto.

```java
public class Persona { 
	private String nombre; // invariante: no es vacío 
	private int edad; // invariante: edad >= 0 
	public Persona(String nombre, int edad) { ... } 
	public String getNombre() { 
		return nombre; 
	} 
	public void setNombre(String nombre) { 
		if (nombre == null || nombre.isEmpty()) { 
			throw new IllegalArgumentException("..."); 
		} 
		this.nombre = nombre; 
	} 
	public int getEdad() { 
		return edad; 
	} 
	public void setEdad(int edad) { 
		if (edad < 0) { 
			throw new IllegalArgumentException("..."); 
		} 
		this.edad = edad; 
	} 
}
```

## Polimorfismo

> [!info]- Definición
> Es la capacidad de representar **múltiples tipos de datos** diferentes mediante **un único símbolo**

Comunmente se reconocen las siguientes categorías de polimorfismo:
- **Polimorfismo ad-hoc**: funciona con un número limitado y conocido de tipos, no necesariamente relacionados entre sí.
	- **Polimorfismo por sobrecarga**.
	- **Polimorfismo por coercion**.
- **Polimorfismo universal**: funciona con un número ilimitado de tipos relacionados entre sí
	- **Polimorfismo paramétrico**.
	- **Polimorfismo por inclusión**.
### Polimorfismo por sobrecarga

Es la capacidad de escribir dos o más funciones o métodos con el **mismo nombre pero diferente firma**

### Polimorfismo por coerción

En programación, *coerción* significa **forzar a que un valor de un tipo sea convertido a otro tipo**.

### Polimorfismo paramétrico (*generics*)

Cuando se usa un símbolo genérico que luego puede ser sustituido por un tipo específico.

```java
public interface Lista<T> {
	void agregar(T element);
	T obtener(int index);
	int cantidad();
}
```

### Polimorfismo por inclusión o de subtipos

Se basa en el hecho de que los tipos de datos forman una **jerarquía**, de forma tal que un objeto de un tipo **subtipo** puede ser tratado como un objeto de su tipo **supertipo**

```java
public interface Lista { 
	void agregar(Object element); 
	Object obtener(int index); int cantidad(); 
} 

public class VectorDinamico implements Lista { ... } 
public class ListaEnlazada implements Lista { ... }  

public void armarListaSupermercado(Lista lista) { 
	lista.agregar("mate"); 
	lista.agregar("café"); 
	lista.agregar("azúcar"); 
	lista.agregar("palmitos"); 
}
```
## Herencia

> [!info]- Definición
> Es un mecanismo que permite **crear nuevas clases basadas en clases existentes, heredando sus atributos y métodos**, y **agregando o modificando funcionalidad.**

A la clase previamente existente se la conoce como ***superclase***, y a las nuevas clases como ***subclases***.

Algunos lenguajes de programación (ej: Java) soportan únicamente la **herencia simple**, donde una subclase hereda de una única superclase, y otros (ej: Python) soportan la **herencia múltiple**, donde una subclase puede heredar de múltiples superclases.

### La herencia y las jerarquías de clases

Una subclase **es más específica que su superclase** y representa a un grupo más especializado de objetos.

A la herencia se la conoce a veces como **especialización** o **generalización**, ya que la subclase exhibe los comportamientos de su superclase junto con los adicionales específicos de esta subclase.

### Redefinición de métodos

Una subclase puede **sobreescribir** o **redefinir** cualquier método de la superclase con una implementación modificada (method overriding).

La palabra clave `super` permite acceder a los atributos y métodos de la superclase.

### La clase Object

En Java, todas las clases heredan directa o indirectamente de la clase `Object` . 
Entre los métodos heredados se destaca `toString()` , que devuelve una representación en forma de cadena del objeto.

### Java: herencia y constructores

Los constructores **no se heredan**.

Si no se define un constructor, todas las clases tienen un **constructor por defecto**: el constructor sin parámetros.

Si en el cuerpo de un constructor no hay una llamada explícita a `super()`, se **invoca implícitamente** como primera instrucción.

De esta manera, cuando se crea un objeto empieza una cadena de llamadas a los constructores, desde la subclase hacia arriba en la jerarquía de herencia, hasta llegar a la clase Object.

Si se declara un constructor con parámetros, **el constructor por defecto deja de estar disponible**.

Es posible sobrecargar el constructor.

### Clases abstractas

Si una clase o alguno de sus métodos está marcado con la palabra clave `abstract`, entonces la clase es **abstracta** y **no puede ser instanciada directamente**.

```java
public abstract class PoligonoRegular { 
	private double lado; 
	public PoligonoRegular(double lado) { this.lado = lado; } 
	public double getLado() { return lado; } 
	public abstract double calcularArea(); 
} 
public class TrianguloEquilatero extends PoligonoRegular { 
	public TrianguloEquilatero(double lado) { super(lado); } 
	@Override public double calcularArea() { return (Math.sqrt(3) / 4) * Math.pow(getLado(), 2); } 
} 
public class Cuadrado extends PoligonoRegular { 
	public Cuadrado(double lado) { super(lado); } 
	@Override public double calcularArea() { return Math.pow(getLado(), 2); } 
}

Public class Main { public static void main(String[] args) { PoligonoRegular tri = new TrianguloEquilatero(5); PoligonoRegular cua = new Cuadrado(4); System.out.println("Área del triángulo: " + tri.calcularArea()); System.out.println("Área del cuadrado: " + cua.calcularArea()); } }
```

### Limitación de la herencia múltiple

El principal problema de la herencia múltiple se conoce como el **problema del diamante**.

![[Pasted image 20260316160020.png]]

¿Qué comportamiento debería tener un vehículo anfibio: el método `avanzar` que hereda de Auto o el que hereda de Lancha?
```java
class Vehiculo { 
	abstract void avanzar(); 
} 
class Auto extends Vehiculo { 
	@Override void avanzar() { ... } 
} 
class Lancha extends Vehiculo { 
	@Override void avanzar() { ... } 
} 
// esto no se permite en Java: 
class VehiculoAnfibio extends Auto, Lancha { } 
VehiculoAnfibio v = new VehiculoAnfibio(); 
v.avanzar();
```

### Limitación de la herencia simple

La inexistencia de la herencia múltiple podría resultar limitante para ciertos diseños.

![[Pasted image 20260316160412.png]]

¿Cómo podemos expresar que un Celular es al mismo tiempo un Telefono y un EnviadorDeMensajes?
¿Y que una PalomaMensajera es un Animal y un EnviadorDeMensajes?