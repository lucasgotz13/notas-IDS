---
id: 1776099844-interfaces-graficas
aliases:
  - Interfaces Graficas
tags:
  - paradigmas
---

# Interfaces Graficas

## REPL vs Event loop

Las CLI suelen ser implementadas mediante un algoritmo simple: [REPL](https://es.wikipedia.org/wiki/REPL)

En las interfaces de usuario TUI/GUI hay que lidiar con múltiples entradas y salidas.
Solución: **[event loop](https://en.wikipedia.org/wiki/Event_loop)**

Los frameworks GUI suelen abstraer el event loop;

## Gráficos, Widgets y aplicaciones

Existe una gran cantidad de opciones de librerías y frameworks gráficos, cada una con sus características, ventajas y desventajas.
Además, hay que considerar el **nivel de abstracción** deseado. Algunos ejemplos:
- **Librerías gráficas (bajo nivel)**: SDL, OpenGL, Vulkan, DirectX. Se encargan de dibujar píxeles en la pantalla.
- **Widget toolkits**: GTK, Qt, Tk, wxWidgets, WinUI, Cocoa. Facilitan la creación de interfaces gráficas.
- **App Frameworks (alto nivel)**: Electron, Tauri, Flutter, JavafX. Proveen un entorno completo para desarrollar aplicaciones. El event loop suele estar abstraído en esta capa.

## Modo inmediato vs modo retenido
### Modo inmediato
- La escena se mantiene en la memoria de la aplicación.
- La aplicación es responsable de invocar a la librería gráfica para re-dibujar la pantalla.
- Las librerías gráficas de bajo nivel suelen ser de modo inmediato.

### Modo retenido
- La escena se mantiene en la memoria de la librería gráfica.
- La librería gráfica se encarga de re-dibujar la pantalla en caso de ser necesario.
- Los frameworks de alto nivel suelen ser de modo retenido.

## Capas de abstracción
Siguiendo el principio **SoC**, las aplicaciones con UI suelen tener al menos 2 o 3 capas de abstracción:
- **Presentación**: Se encarga de la interacción con el usuario.
- **Lógica de negocio**: Se encarga de modelar el estado de la aplicación y las operaciones que pueden realizarse sobre él.
- **Persistencia**: Se encarga de **almacenar** el estado de la aplicación de forma permanente, por ejemplo en una base de datos o un archivo.

## JavaFX
Es un framework para crear aplicaciones sobre la plataforma Java.

### Scene Graph

El **Scene Graph** es la estructura de datos y API asociada de JavaFX para manipular la escena. Es similar al **DOM**: los elementos forman un árbol y los eventos se propagan a través de él.

![[Pasted image 20260413151243.png]]

- **Stage**: Representa una ventana en la pantalla. Contiene un **Scene**
- **Scene**: Representa el contenido de la ventana. Contiene el **Scene Graph**, mediante una referencia al nodo raíz.
- **Node**: Clase base para todos los nodos del **Scene Graph**.
- **Parent**: Clase base para los nodos que pueden tener hijos.

#### Layout
Estas clases permiten agrupar nodos para posicionar y redimensionar con diferentes estrategias.

#### Controles
Son los componentes interactivos de la interfaz de usuario, como botones, etiquetas, campos de texto, etc.

#### Shapes
Permiten dibujar formas geométricas básicas como líneas, círculos, rectángulos, polígonos, etc.

El **Canvas** es más eficiente para dibujar gráficos complejos, ya que permite dibujar directamente en un área rectangular, sin necesidad de crear un nodo para cada forma. Es útil para gráficos dinámicos o animaciones.

### Properties & Bindings
Las clases del paquete `javafx.beans.property` ofrecen interfaces e implementaciones de **properties** que encapsulan valores que pueden ser **observados** y **enlazados** (bindings)
