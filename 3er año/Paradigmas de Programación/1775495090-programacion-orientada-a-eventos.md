---
id: 1775495090-programacion-orientada-a-eventos
aliases:
  - Programacion orientada a Eventos
tags:
  - paradigmas
---

# Programación orientada a Eventos

> [!Info]- Definicion
> Es un paradigma de programación en el que el **flujo del programa** es determinado por la ocurrencia de eventos, que son previstos pero no planeados (no se saben cuando ocurriran)

Ejemplo => GUIs => Se deben manejar eventos como clics de ratón, pulsaciones de teclado, etc.
Dos tipos de objetos:
- **Objeto que produce eventos**: Event source, Event emitter, Event dispatcher, Publisher
- **Objeto que quiere ser notificado**: Listener, Subscriber, Consumer

## Estrategia de polling
- Esta estrategia es **sincrónica**: Las operaciones ocurren en un orden determinado.

## Callbacks

> [!Info]- Definicion
> Es una función que se pasa como parámetro a otra función (típicamente **no bloqueante**). El callback será invocado en algún momento posterior (es decir, en forma **asincrónica**), por ejemplo cuando ocurre un evento.

- Esta estrategia es de tipo **push**: El emisor "empuja" los eventos a los consumidores.
- En Java, el pasaje de callbacks se realiza mediante clases abstractas o interfaces.
- Los callbacks suelen ser llamados **handlers** cuando son utilizados para manejar eventos.

```java
public class Main {
	public static void main(String[] args) { 
		Timer timer = new Timer(); 
		TimerTask callback = new TimerTask() { 
			int segundos = 0; 
			@Override public void run() { 
				System.out.printf("Pasaron %ds.\n", segundos++);
			} 
		}; 
		// callback.run() será invocado cada 1 segundo 
		timer.scheduleAtFixedRate(callback, 0, 1000); 
		// El mensaje anterior fue no bloqueante 
		System.out.println("Timer configurado."); 
	} 
}
```

## Entrada/Salida multiplexada
Esta estrategia consiste en bloquear la ejecución hasta que ocurra algún evento de interés en alguno de los archivos monitoreados.

## Entrada/Salida no bloqueante
Otra estrategia para manipular múltiples archivos es la de **entrada/salida no bloqueante**, en la que las funciones de lectura y escritura no bloquean la ejecución, sino que se ejecutan en segundo plano. La notificación de la finalización de la operación ocurre en forma **asincrónica** mediante callbacks.

## Patrón Observer
Es un patrón de diseño de POO que permite registrar múltiples **callbacks** para ser invocados cuando ocurra un evento. De esta manera se logra una comunicación **uno a muchos** (un emisor, múltiples observadores).

![[Pasted image 20260406153828.png]]

### Ejemplo
```java
public interface Observador { 
	public void nivelGanado(); 
} 

public class Juego { 
	private List observadores = new ArrayList<>(); 
	public void suscribir(Observador obs) { 
		observadores.add(obs); 
	} 
	
	public void notificarNivelGanado() { 
		for (Observador obs : observadores) { 
			obs.nivelGanado(); 
		} 
	} 
}

public class Logros implements Observador { 
	@Override public void nivelGanado() { 
		System.out.println("¡Nuevo logro: Nivel ganado!"); 
	} 
} 

public class UI implements Observador {
	@Override public void nivelGanado() { 
		System.out.println("UI: Nivel ganado."); 
	} 
} 

Juego juego = new Juego(); 
Logros logros = new Logros(); 
UI ui = new UI(); 

juego.suscribir(logros); 
juego.suscribir(ui); 

// Simular que se gana un nivel 
juego.notificarNivelGanado();
```

## Event loop
Es una estrategia que permite desacoplar aun más los emisores de los consumidores. La publicación de los eventos es asincrónica con la invocación de los handlers.

![[Pasted image 20260406154951.png]]
