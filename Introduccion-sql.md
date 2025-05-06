---
id: 1745495822-introduccion-sql
aliases:
  - Introduccion SQL
tags:
  - intro-desarrollo
---

# Introduccion SQL

## Comandos Básicos de SQL

```sql
CREATE DATABASE base_dedatos; -- Crea una base de datos
DROP DATABASE base_dedatos; -- Elimina una base de datos

CREATE TABLE usuarios(id INT, nombre VARCHAR(50), apellido VARCHAR(50)); -- Crea una tabla de usuarios
DROP TABLE usuarios; -- Elimina la tabla de usuarios

INSERT INTO usuarios (id, nombre, apellido)
VALUES (1, "Lucas", "Gotz Baliner");
```
