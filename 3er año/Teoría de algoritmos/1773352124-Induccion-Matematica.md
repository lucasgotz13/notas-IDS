---
id: 1773352124-Induccion-Matematica
aliases:
  - Induccion Matematica
tags:
  - tda
---

# Inducción Matemática

## Implicaciones lógicas

H => T "Si H entonces T"
Si H es falsa, la implicación es verdadera.
Si T es verdadera, la implicación es verdadera.
Si H es verdadera, entonces T debe ser verdadera.

H => T = ¬H v (H ^ T)

Hay diferentes formas de probar esto:
1. Método directo
2. Método indirecto
3. Por el absurdo/contradicción
4. Inducción

### Método directo
Asumimos que H es verdadera y demuestro que T también lo es
### Método indirecto
Demostramos que si T es falso, h es falso.
### Por el absurdo
Asumimos que H es verdadera y T es falsa y llegamos a una contradicción
### Principio de Inducción Matemática
Se puede demostrar por inducción la proposición $P(n)$ ($n \in \mathbb{N}_0$)
1. Se demuestra que $P(n_0)$ es verdadero (paso base)
2. $\forall h \ge n_0 : v[P(h) \rightarrow P(h+1)] = V$ (paso inductivo)