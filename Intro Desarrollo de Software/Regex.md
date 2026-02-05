---
id: Regex
aliases:
  - regex
tags:
  - intro-desarrollo
---
#intro-desarrollo 
# Regex

- (expresion1|expresion2) -> Muestra las palabras que coincidan con la expresion1 O con la expresion2
- . -> Comodín. Matchea todo tipo de caractér.
- [] -> Colección. Parecido al grupo. Matchea a toda palabra que matchee con al menos uno de los caracteres que este dentro de la coleccion.
	- El grupo busca literal. La colección no.
- a-z, A-Z, 0-9 -> Son rangos. Matchean todo lo que este dentro de esos rangos (generalmente es usado dentro de las colecciones) ![[Pasted image 20250502232012.png]]
- Tokens
	- \n -> Nueva línea
	- \t -> Tabulación
	- \s -> Cualquier carácter de espacio en blanco.
	- \S -> Cualquier carácter que NO sea un espacio en blanco
	- \w -> Cualquier carácter de palabra (letras, números y _ )
	- \W -> Cualquier carácter que NO sea de palabra
	- \b -> Límite de palabra. Coincide en los espacios entre caractéres
	- \B -> El inverso de \b
	- ^ (dentro de colección) -> NIEGA el contenido
	- ^ (fuera de colección) -> El inicio de una linea
	- $ -> El final de una línea
	- \ -> El carácter literal
- Cuantificadores
	- {4} -> Coincide con las palabras de 4 carácteres
	- {2,4} -> Coincide con las palabra de 2 a 4 carácteres
	- {,4} -> Coincide con las palabras de 4 carácteres o menos
	- {4,} -> Coincide con las palabras de 4 carácteres o más.
	- expresión* -> coincide con 0 o más de con el tipo de expresión
	- expresión+ -> coincide con 1 o más de con el tipo de expresión
	- expresión? -> coincide con 0 o 1 de con el tipo de expresión
## Preguntas
¿Qué hace la expresión `(expresion1|expresion2)` en regex?::Coincide con las palabras que coincidan con **expresion1 O expresion2**.

¿Qué significa el punto `.` en regex?::Es un **comodín** que matchea **cualquier carácter**.

¿Qué hacen los corchetes `[]` en regex?::Definen una **colección**: coincide con cualquier carácter que esté **dentro del conjunto**.

¿Cuál es la diferencia entre grupo y colección en regex?::El **grupo** busca coincidencia **literal**, mientras que la **colección** coincide con **cualquier carácter del conjunto**.

¿Qué representan `a-z`, `A-Z` y `0-9` en regex?::Son **rangos** que coinciden con letras minúsculas, mayúsculas o números, comúnmente usados dentro de colecciones.


¿Qué hace el token `\n` en regex?::Coincide con un **salto de línea**.

¿Qué hace el token `\t` en regex?::Coincide con una **tabulación**.

¿Qué hace `\s` en regex?::Coincide con **cualquier carácter de espacio en blanco**.

¿Qué hace `\S` en regex?::Coincide con **cualquier carácter que NO sea espacio en blanco**.

¿Qué hace `\w` en regex?::Coincide con **cualquier carácter de palabra**: letras, números y guión bajo `_`.

¿Qué hace `\W` en regex?::Coincide con **cualquier carácter que NO sea de palabra**.

¿Qué hace `\b` en regex?::Coincide con un **límite de palabra**, es decir, los espacios entre caracteres.

¿Qué hace `\B` en regex?::Es el **inverso de `\b`**, coincide donde **no** hay límite de palabra.

¿Qué significa `^` dentro de una colección `[^abc]`?::**Niega** el contenido de la colección; matchea cualquier carácter que **no esté dentro**.

¿Qué significa `^` fuera de una colección?::Indica el **inicio de una línea**.

¿Qué significa `$` en regex?::Indica el **final de una línea**.

¿Qué hace la barra invertida `\` en regex?::Escapa un carácter para que sea **interpretado literalmente**.


¿Qué hace `{4}` como cuantificador?::Coincide con palabras de **exactamente 4 caracteres**.

¿Qué hace `{2,4}` como cuantificador?::Coincide con palabras de **2 a 4 caracteres**.

¿Qué hace `{,4}` como cuantificador?::Coincide con palabras de **hasta 4 caracteres**.

¿Qué hace `{4,}` como cuantificador?::Coincide con palabras de **4 o más caracteres**.

¿Qué hace `expresión*` en regex?::Coincide con **0 o más repeticiones** de la expresión.

¿Qué hace `expresión+` en regex?::Coincide con **1 o más repeticiones** de la expresión.

¿Qué hace `expresión?` en regex?::Coincide con **0 o 1 repetición** de la expresión.