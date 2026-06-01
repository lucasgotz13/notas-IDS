---
id: 1779912949-programacion-concurrente
aliases:
  - Programacion Concurrente
tags:
  - paradigmas
---

# Programación Concurrente en Java

## Concurrencia y Paralelismo

> [!Info]
> **Concurrencia** es la habilidad de lidiar con múltiples tareas que pueden estar en progreso al mismo tiempo (pero no necesariamente en ejecución).

> [!Info]
> **Paralelismo** es la habilidad de ejecutar múltiples tareas en forma simultánea. Requiere soporte de hardware (múltiples CPUs o cores).

## I/O bound vs CPU bound

Los programas generalmente se pueden categorizar en dos tipos:

> [!Info]
> Un programa es **I/O bound** cuando hace uso intensivo de operaciones de entrada/salida.

No suele beneficiarse mucho del paralelismo

> [!Info]
> Un programa es **CPU bound** cuando hace uso intensivo del CPU.

Suele beneficiarse más del paralelismo.

## Procesos

Son unidades de ejecución independientes y aisladas, con su propio espacio de memoria.

Son manejados por el sistema operativo. El **scheduler** (planificador) es el componente del SO que asigna tiempo de CPU a cada proceso (y en el caso de sistemas multicore, asigna los diferentes core).

Para comunicarse entre sí, los procesos requieren mecanismos de IPC (_comunicación inter-proceso_) provistos por el SO, como **pipes** o **sockets**.

### Ejemplo: Sockets

Servidor:

```java
try (ServerSocket serverSocket = new ServerSocket(1234)) {
  Socket clientSocket = serverSocket.accept();
  BufferedReader in = new BufferedReader(
    new InputStreamReader(clientSocket.getInputStream())
  );
  String line = in.readLine();
  // ...
}
```

Cliente:

```java
try (Socket clientSocket = new Socket("localhost", 1234)) {
  PrintWriter out = new PrintWriter(
    clientSocket.getOutputStream(),
    true
  );
  out.println("hola");
}
```

![[Pasted image 20260527181830.png]]

## Hilos

Son unidades de ejecución dentro de un proceso

Comparten el mismo espacio de memoria.

Pueden ser manejados por el sistema operativo o por la propia aplicación (dependiendo del lenguaje y la biblioteca de threads utilizada).

### Hilos en Java

La clase `Thread` representa un hilo de ejecución en Java.

```java
public class Main {
  public static void main(String[] args) {
    Thread t = new Thread(() -> {
      System.out.println("Hola desde el hilo!");
    });
    t.start(); // Inicia el hilo
    System.out.println("Hola desde el hilo principal!");
  }
}
```

El proceso finaliza cuando no queda ningún hilo de tipo _non-daemon_ en ejecución.

### Estados de los hilos en Java

![[Pasted image 20260527190735.png]]

### Sincronización usando _interrupt_ y join

![[Pasted image 20260527191010.png]]

## Condiciones de carrera

Condición de carrera => [[1777818648-memoria-ii#Race conditions|Race conditions]]

La JVM define un **modelo de memoria** que especifica cómo y cuándo los cambios hechos por un hilo son visibles para otros hilos.

> [!note]
> Una función u objeto es _thread-safe_ si puede ser utilizado por múltiples hilos sin condiciones de carrera.

## Sincronización: Candados

> [!Info]
> Un **candado** (_lock_/_mutex_) es un mecanismo de sincronización que permite a los hilos coordinar el acceso a recursos compartidos, previniendo race conditions

### Locks en Java

Todos los mecanismos de sincronización en Java se construyen en base a un **candado intrínseco** (o **monitor**) asociado a cada objeto.

Al entrar al bloque `synchronized(candado) {...}` el hilo intenta **adquirir** el candado intrínseco del objeto `candado`.

- Si el candado está libre, el hilo lo adquiere y entra al bloque.
- Si el candado está ocupado por otro hilo, el hilo actual se **bloquea** hasta que el candado se libere.

Al finalizar el bloque, el hilo **libre** el candado.

```java
class Main {
  static int a = 0;
  static Object candado;
  static void incThread() {
    for (int i = 0; i < 100000; i++) {
      synchronized(candado) {
        a++;
      }
  }
 }
  static void decThread() {
    for (int i = 0; i < 100000; i++) {
      synchronized(candado) {
        a--;
      }
    }
  }
}
```

Azúcar sintáctica:

```java
public class ContadorSincronizado {
  private int c = 0;

  public synchronized void incrementar() {
    c++;
  }

  public synchronized int valor() {
    return c;
  }
}
```

##
