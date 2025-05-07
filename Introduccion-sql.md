---
id: 1745495822-introduccion-sql
aliases:
  - Introduccion SQL
tags:
  - intro-desarrollo
---

# Introduccion SQL

## ¿Qué son las Bases de Datos?

- Nos permiten generar un almacenamiento organizado de información.
- Facilitan la búsqueda, recuperación y gestión de datos.
- Son esenciales para aplicaciones web.
### Características de una base de datos
- Base de datos: Contenedor de objetos (tablas, vistas, etc).
- Motor de base de datos: Núcleo del sistema, encargado del almacenamiento y recuperación de datos.
	- Ejemplos
		- PostgreSQL: Open source, potente y flexible.
		- MySQL: Open source, ampliamente utilizado.
		- SQL Server: De Microsoft. Enfocado en entornos empresariales
- Gestor de base de datos: Software que interactúa con la base de datos.
	- Ejemplos
		- DBeaver
		- pgAdmin
		- Terminal
## ¿Qué es y para qué sirve SQL?

SQL (Structured Query Language) es el lenguaje estándar para gestionar bases de datos relacionales.
Permite:
- **Crear y modificar** bases de datos.
- **Definir** estructuras de tablas.
- **Insertar**, **modificar** y **eliminar** datos.
- **Consultar información** de manera eficiente.
## Comandos Básicos de SQL

```postgresql
CREATE DATABASE base_dedatos; -- Crea una base de datos
DROP DATABASE base_dedatos; -- Elimina una base de datos

CREATE TABLE usuarios(id INT, nombre VARCHAR(50), apellido VARCHAR(50)); -- Crea una tabla de usuarios
DROP TABLE usuarios; -- Elimina la tabla de usuarios

INSERT INTO usuarios (id, nombre, apellido)
VALUES (1, 'Lucas', 'Gotz Baliner');

DELETE FROM usuarios WHERE id = 1; -- Elimina el registro de la tabla

UPDATE clientes SET apellido = 'Garcia' WHERE id = 2; -- Modifica el registro especificado

```


## Segunda clase

#### primary key
Nos permite hacer busquedas de forma mas fácil y rápidas a través del campo que contenga PRIMARY KEY (En general es el 'id').

#### serial
Es una secuencia que autoincrementa un campo. Generalmente es usado en los campos id.

Ejemplo:
```postgresql
CREATE TABLE usuarios(
	id serial primary key, -- Va a generar ids secuencialmente 
	nombre VARCHAR(50),
	apellido VARCHAR(50)
);
```

#### foreign key
Es un valor que en otra tabla que en otra tabla es una clave primaria

Ejemplo:
```postgresql
create table pagos(
	...
	id_usuario int references usuarios(id)
);
```

#### order by
comando que permite ordenar las tablas por los valores de determinado campo
#### limit
Comando que hace que la query devuelva los primeros n resultados (ejemplo: limit 3 te devuelve los primeros 3 resultados).
#### sum
Devuelve la suma de todos los registros que coinciden con la query
#### count
Devuelve la cantidad total de registros que coinciden con la query
#### otras funciones de agregacion
- MAX
- MIN

ORDER BY y LIMIT actuan sobre el resultado, mientras que SUM y COUNT nos da un valor
#### funciones comparadoras
- AND
- OR
- BETWEEN
#### sUBSELECTS
Las subselects tienen que dar **un solo** valor.
Lógica:
Por cada registro de tal tabla, hace una consulta de tal otra tabla.
#### Group by
Permite hacer **comparaciones entre agrupamientos** en una sola query.
#### having
Filtra los resultados de los agrupamientos (similar al while)
#### distinct
Nos da todos los valores distintos de una columna (Osea, si por ejemplo hay 5 registros con el mismo valor devuelve uno solo)
#### JOINS
Permite hacer consultas que muestre información de varias tablas.
![[images.png]]
### Ejemplos
```postgresql
-- Selecciona el torneo con mayor premio
select *
from torneos
order by premio desc
limit 1;

-- Selecciona el total pagado en premios
select sum(premio)
from torneos
where id_ganador is not null;

-- Obtiene la cantidad de ganadores
select count(*)
from torneos
where id_ganador is not null;

select * from personajes
where raza = 'Humano' and ki > 50000 -- ejemplo de and

select * from personajes
where raza = 'Humano' or ki < 50000 -- ejemplo de or

select * from personajes p
where (p.raza = 'Humano' and ki > 50000)
or (p.raza != 'Humano' and ki < 5000)  
order by raza asc, ki desc;

select * from personajes
where ki between 10000 and 60000 -- Ejemplo de between
order by ki desc;

select nombre, (select nombre from personajes where id = id_ganador)
from torneos; -- Ejemplo de subselect

select max_concursantes, max(premio), min(premio), sum(premio)
from torneos
group by max_concursantes;

select raza, count(*)
from personajes
group by raza
having(*) >= 10
order by count(*) desc; -- ejemplo de having

select distinct raza
from personajes;

select * from torneos t
inner join personajes p on t.id_ganador = p.id

select * from torneos t
left join personajes p on t.id_ganador = p.id

select * from torneos t
right join personajes p on t.id_ganador = p.id

select * from torneos t
full outer join personajes p on t.id_ganador = p.id

select * from torneos t, personajes p
where t.id_ganador = p.id; -- Form simplificada del inner join
```

## Preguntas
#sql/teorico
¿Qué nos permiten las Bases de Datos?::Nos permiten generar un almacenamiento organizado de información, facilitan la búsqueda, recuperación y gestión de datos y son muy útiles para aplicaciones web.
¿Cuáles son las características de una Base de Datos?
?
- Base de datos: Contenedor de objetos (tablas, vistas, etc).
- Motor de base de datos: Núcleo del sistema, encargado del almacenamiento y recuperación de datos. Ejemplos: PostgreSQL, MySQL, etc.
- Gestor de Base de Datos: Software que interactúa con la base de datos. Ejemplos: DBeaver, pgAdmin, etc.

¿Qué es SQL?::SQL (Structured Query Language) es el lenguaje estándar para gestionar bases de datos relacionales.
¿Qué permite SQL?
?
Permite:
- **Crear y modificar** bases de datos.
- **Definir** estructuras de tablas.
- **Insertar**, **modificar** y **eliminar** datos.
- **Consultar información** de manera eficiente.


#sql/comandos-basicos
¿Cómo se crea una base de datos?::create database base_de_datos;
¿Cómo se borra una base de datos?::drop database base_de_datos;
¿Cómo se crea una tabla?::create table usuarios(id INT, nombre VARCHAR(50), apellido VARCHAR(50));
¿Cómo se borra una tabla?::drop table usuarios;
¿Cómo se insertan registros a una tabla?::`insert into usuarios values (1, 'Lucas', 'Gotz')`;
¿Cómo se eliminan registros de una tabla?::`delete from usuarios where id = 1`;
¿Cómo se modifican registros de una tabla?::`update usuarios set apellido = 'García' where id = 1;`

#sql/funciones

¿Qué hace la función 'order by' y 'limit'?
?
Order by: Comando que permite ordenar las tablas por los valores de determinado campo
Limit: Comando que hace que la query devuelva los primeros n resultados (ejemplo: limit 3 te devuelve los primeros 3 resultados).
```postgresql
select *
from torneos
order by premio desc
limit 1;
```

¿Qué hace la función 'sum'?
?
Devuelve la suma de todos los registros que coinciden con la query
```postgresql
-- Obtiene la cantidad de ganadores
select sum(premio)
from torneos
where id_ganador is not null;
```

¿Qué hace la función 'count'?
?
Devuelve la cantidad total de registros que coinciden con la query
```postgresql
-- Obtiene la cantidad de ganadores
select count(*)
from torneos
where id_ganador is not null;
```

Dime un ejemplo de la funcion and/or
?
```postgresql
select * from personajes
where raza = 'Humano' and ki > 50000 -- ejemplo de and

select * from personajes
where raza = 'Humano' or ki < 50000 -- ejemplo de or
```

Dime un ejemplo de la funcion between
?
```postgresql
select * from personajes
where ki between 10000 and 60000 -- Ejemplo de between
order by ki desc;
```

Que hacen los subselects
?
Las subselects tienen que dar **un solo** valor.
Lógica:
Por cada registro de tal tabla, hace una consulta de tal otra tabla.
```postgresql
select nombre, (select nombre from personajes where id = id_ganador)
from torneos; -- Ejemplo de subselect
```

¿Qué hace la función 'group by'?
?
Permite hacer **comparaciones entre agrupamientos** en una sola query.
```postgresql
select max_concursantes, max(premio), min(premio), sum(premio)
from torneos
group by max_concursantes;
```

¿Qué hace la función 'having'?
?
Filtra los resultados de los agrupamientos (similar al while)
```postgresql
select raza, count(*)
from personajes
group by raza
having(*) >= 10
order by count(*) desc; -- ejemplo de having
```

¿Para qué sirve la funcion distinct?
?
Nos da todos los valores distintos de una columna (Osea, si por ejemplo hay 5 registros con el mismo valor devuelve uno solo)
```postgresql
select distinct raza
from personajes;
```

¿Para qué sirven los joins?
?
Permite hacer consultas que muestre información de varias tablas.
Tipos:
- Left join
- Right join
- Inner join
- Full Outer Join
```postgresql
select * from torneos t
inner join personajes p on t.id_ganador = p.id

select * from torneos t
left join personajes p on t.id_ganador = p.id

select * from torneos t
right join personajes p on t.id_ganador = p.id

select * from torneos t
full outer join personajes p on t.id_ganador = p.id

select * from torneos t, personajes p
where t.id_ganador = p.id; -- Form simplificada del inner join
```