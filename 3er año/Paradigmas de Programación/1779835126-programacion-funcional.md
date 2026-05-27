---
id: 1779835126-programacion-funcional
aliases:
  - Programacion Funcional
tags:
  - paradigmas
---

# Programacion Funcional

- [[#Características del paradigma funcional|Características del paradigma funcional]]
- [[#Machete de Clojure|Machete de Clojure]]
- [[#Funciones puras|Funciones puras]]
- [[#Transparencia referencial|Transparencia referencial]]
- [[#Datos inmutables|Datos inmutables]]
- [[#Funciones como ciudadanos de primera clase|Funciones como ciudadanos de primera clase]]
- [[#Funciones de orden superior|Funciones de orden superior]]
- [[#Recursión|Recursión]]
- [[#Evaluación perezosa|Evaluación perezosa]]
- [[#Estructuras de datos funcionales|Estructuras de datos funcionales]]

Recordemos: [[1773076782-Introduccion#Paradigmas de Programación|Paradigmas de programación]]

## Características del paradigma funcional

- Funciones puras
- Transparencias referencial
- Datos inmutables
- Las funciones son ciudadanos de primera clase
- Funciones de orden superior
- Recursión
- Evaluación perezosa
- Estructuras de datos funcionales

## Machete de Clojure

Literales:

```clojure
1
nil
true
un-simbolo
:un-keyword
"una cadena"
["un" "vector" "de" "cadenas"]
("una" "lista" "de" "cadenas")
{:tipo "mapa" :clave "valor"}
#{"un conjunto" "de cadenas"}
```

Las listas se interpretan como una **aplicación de función** `(funcion arg1 arg2 ...)`:

```clojure
(+ 1 2) ; => 3
(str "Hola" " mundo!") ; => "Hola mundo!"
(1 2 3) ; => error
'(1 2 3) ; => (1 2 3)
```

Formas especiales:

```clojure
(def pi 3.14159)
(def suma (fn [a b] (+ a b)))
(defn suma [a b] (+ a b)) ; equivalente
(def suma #(+ %1 %2)) ; función anónima

(if (> 3 2)
 (println "Tres es mayor que dos")
 (println "Tres no es mayor que dos"))

(let [x 10 y 20]
 (println "La suma es:" (+ x y)))
```

## Funciones puras

> [!Info] Una **función pura** es aquella que cumple con las siguientes propiedades:
>
> - **Comportamiento determinístico**: Para argumentos idénticos siempre produce valores de retorno idénticos
> - **No produce efectos colaterales**.

![[Pasted image 20260526215046.png]]

## Transparencia referencial

> [!info] Una expresión es **referencialmente transparente** si puede ser reemplazada por su valor sin cambiar el comportamiento del programa.

Las funciones puras son referencialmente transparentes, lo que permite razonar acerca del código y modificarlo sin efectos inesperados.

Ejemplo: ¿El valor de `y` es el mismo en ambos casos?

![[Pasted image 20260526215429.png]]

Si `f` es una función pura, entonces ambas expresiones son equivalentes (salvando una posible diferencia en eficiencia).

## Datos inmutables

> [!info] Un programa funcional puro opera exclusivamente con datos inmutables.

En lugar de alterar valores existentes, se crean copias alteradas y se preserva el original.

Ejemplo

![[Pasted image 20260526220039.png]]

## Funciones como ciudadanos de primera clase

En la programación funcional, las funciones son **ciudadanos de primera clase** . Esto significa que pueden ser tratadas como cualquier otro valor: pueden ser asignadas a variables, pasadas como argumentos y devueltas como resultados.

```clojure
(let [x 2
      f (fn [y] (+ x y))]
  (f 3))
```

En el ejemplo, la función anónima es una **clausura** que captura el valor de `x` del entorno donde fue definida.

## Funciones de orden superior

> [!Info] Una **función de orden superior** es aquella que puede recibir funciones como argumentos o devolver funciones como resultado.

```clojure
(defn dos-veces [f x] (f (f x)))

(println (dos-veces inc 5)) ; 7
(println (dos-veces #(str % "!") "Hola")) ; "Hola!!"
```

Las funciones `map`, `filter` y `reduce` son ejemplos comunes de funciones de orden superior que operan sobre colecciones.

```clojure
(map inc [1 2 3]) ; (2 3 4)
(filter even? [1 2 3 4]) ; (2 4)
(reduce + [1 2 3 4]) ; 10
```

## Recursión

En los lenguajes funcionales, la iteración (ciclos) se logra mediante la **recursión**.

Si la llamada recursiva está en **posición de cola**, se puede usar `recur`.

De esta forma, el compilador puede optimizar la llamada recursiva y evitar el crecimiento del _stack_.
La forma especial `loop` también se puede usar para crear un punto de recursión explícito sin necesidad de definir una función auxiliar.

## Evaluación perezosa

> [!Info]
> La **evaluación perezosa** (lazy evaluation) es una estrategia de evaluación de expresiones que retrasa la evaluación de una sub-expresión hasta que su valor sea realmente necesario.

Clojure no tiene evaluación perezosa por defecto, pero proporciona mecanismos para crear y manipular **secuencias perezosas**

![[Pasted image 20260526223932.png]]

## Estructuras de datos funcionales

> [!info]
> Las estructuras de datos funcionales, o **estructuras de datos persitentes**, son aquellas que siempre preservan la versión anterior ante cualquier modificación.

Estas estructuras de datos son efectivamente **inmutables**.

Las colecciones provistas por Clojure cumplen con esta propiedad.

```clojure
(def xs '(0 1 2))
(def ys '(3 4 5))
(def zs (concat xs ys))
```

![[Pasted image 20260526230030.png]]
