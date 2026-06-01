---
id: 1779749293-calculo-lambda
aliases:
  - Calculo Lambda
tags:
  - paradigmas
---

# Calculo Lambda

- [[#Funciones|Funciones]]
- [[#Cálculo Lambda|Cálculo Lambda]]
- [[#Simplificaciones|Simplificaciones]]
- [[#Variables libres y ligadas|Variables libres y ligadas]]
- [[#Reglas de reducción|Reglas de reducción]]
- [[#Forma normal|Forma normal]]
- [[#Estrategias de reducción|Estrategias de reducción]]
- [[#Codificación de tipos de datos|Codificación de tipos de datos]]
  - [[#Codificación de tipos de datos#Booleanos|Booleanos]]
  - [[#Codificación de tipos de datos#Numerales de Church|Numerales de Church]]

## Funciones

El Cálculo Lambda incorpora dos simplifiaciones para operar con funciones:

1. **Las funciones son anónimas**. Por ejemplo, la función:
   $$
   suma\_cuadrados(x,y) = x^{2}+y^{2}
   $$
   se puede escribir como $(x,y) \implies x^2 + y^2$
2. **Todas las funciones son de un solo argumento.** Por ejemplo, la función:
   $$
   (x,y) \implies x^2+y^2
   $$
   Se puede escribir como
   $$
    x \implies (y \implies x^2 + y^2)
   $$
   Esta transformación se llama _currificación_ (por Haskell Curry)

## Cálculo Lambda

Consiste en escribir **expresiones lambda** con una sintaxis formal, y aplicar **reglas de reducción** para transformarlas.

> [!info] Una **expresión lambda** puede ser:
>
> - Una **variable**.
> - Una **abstracción**: (λx.M) donde M es una expresión lambda.
> - Una **aplicación**: (M N) donde M y N son expresiones lambda.

Ejemplo: `(((λx.(x y)) (λy.(y y))) z)`

Una abstracción denota una función anónima que toma un argumento `x` y devuelve `M`, es decir, $x \implies M$

Una aplicación (M N) denota la acción de _invocar_ la función `M` con el argumento `N`, es decir, $M(N)$

## Simplificaciones

Para simplificar la notación:

1. Se pueden omitir los paréntesis externos: `(M N) === M N`
2. Las aplicaciones se asocian a la izquierda: `((M N) P) === M N P`
3. El cuerpo de la abstracción se extiende todo lo posible hacia la derecha: `λx.(M N) === λx.M N`
4. Se pueden contraer múltiples abstracciones lambda: `λx.λy.λz.N === λx y z.N`
5. Cuando todas las variables son de una única letra, se pueden omitir los espacios: `M N P === MNP`

## Variables libres y ligadas

Una abstracción `λx.M` **liga** las variables `x` que aparecen en el cuerpo `M`. Todas las demás variables en `M` son **libres**.
![[Pasted image 20260525220024.png]]

- `@` Significa aplicación
- `λ` Significa abstracción

## Reglas de reducción

**Conversión Alfa (α)**: Cambiar variables ligadas

- En la abstracción `λx.M`, se puede cambiar `x` por cualquier otra variable que no aparezca libre en `M`.
- Por ejemplo, `λx.x y =α λz.z y`.

**Reducción Beta (β)**: Aplicar una β-redex

- Una **β-redex** es una aplicación de la forma `(λx.M) N`.
- Por ejemplo, `(λu.u z u) a =β a z a`.

**Reducción Eta (η)**: Reducir una η-redex

- Una **η-redex** es una expresión de la forma `λx.M x` donde `x` no aparece libre en `M`.
- Según la regla n, `λx.M x =n M`.

## Forma normal

Una expresión lambda está en:

- **Forma β-normal**: Si no contiene ninguna β-redex.
  Ejemplo: `z (λx.y x) w`

  > [!Info] La forma β-normal de una expresión, si existe, es única.

- **Forma β-n-normal**: Si no contiene ninguna β-redex ni n-redex
  Ejemplo: `z (λx.x) w`
- **Forma normal de cabecera**: Si no hay una β-redex en la cabeza de la expresión.
  Ejemplo: `z ((λx.x) w)`

## Estrategias de reducción

Si una expresión contiene más de una redex, ¿cuál se debe reducir primero?

Entre las estrategias más comunes están:
**Orden normal**: siempre se reduce la beta-redex más externa y a la izquierda.

- Si la expresión tiene forma normal, esta estrategia la encuentra.

**Orden aplicativo**: Siempre se reduce la beta-redex mas **interna** y a la izquierda.

- Esta estrategia puede no terminar, incluso si la expresión tiene forma normal.

**Call by value**: Como el orden aplicativo, pero no se aplican dentro de abstracciones.

- Esta estrategia es la más común en lenguajes de programación tradicionales con **evaluación ansiosa** (C, Python, Java...): los argumento de una función se evalúan antes de llamar a la función

**Call by name**: Como el orden normal, pero no se aplican reducciones dentro de abstracciones.

- Esta estrategia y otras similares, son comunes en lenguajes funcionales con **evaluación perezosa** como Haskell: las funciones reciben expresiones sin evaluar, y las evalúan solo cuando las necesitan.

## Codificación de tipos de datos

### Booleanos

```lambda
True = λx y.x
False = λx y.y

Not = λp.p False True
And = λp q.p q False
Or = λp q.p True q
If = λp q r.p q r
```

### Numerales de Church

```lambda
0 = λf x.x
1 = λf x.f x
2 = λf x.f (f x)
3 = λf x.f (f (f x))

Succ = λn.λf x.f (n f x)
Pred = λn.λf.λ.n (λg.λh.h (g f)) (λu.x) (λu.u)

Add = λm n.λf x.m f (n f x)
Sub = λm n.n Pred m
Mul = λm n.λf x.m (n f) x
Pow = λm n.λf x.n m f x

IsZero := λn.n (λx.False) True
Leq := λm n.IsZero (Sub m n)
```
