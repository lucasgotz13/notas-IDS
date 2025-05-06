---
id: Regex
aliases:
  - regex
tags:
  - intro-desarrollo
---
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