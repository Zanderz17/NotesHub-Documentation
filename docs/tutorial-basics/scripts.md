---
sidebar_position: 2
---

# Scripts.sql

## Descripción General

Estas instrucciones SQL describen la creación de tablas relacionadas con el manejo de usuarios y límites de resúmenes en una base de datos. Las tablas están diseñadas para almacenar información sobre los usuarios, sus límites de resúmenes y el recuento de interacciones.

## Tabla user_summary_limits

- La tabla user_summary_limits se utiliza para almacenar información sobre los límites de resúmenes personalizados para usuarios específicos.
- La columna user_id es una clave primaria que identifica de manera única a cada usuario.
- La columna first_name almacena el nombre del usuario.
- La columna summary_limit almacena el límite de resúmenes para el usuario.

```sql
CREATE TABLE user_summary_limits (
  user_id BIGINT PRIMARY KEY,
  first_name TEXT,
  summary_limit INT
);
```

## Tabla users

- La tabla users se utiliza para almacenar información general sobre los usuarios, incluidos sus límites de resúmenes y recuento de interacciones.
- La columna user_id es una clave primaria que identifica de manera única a cada usuario.
- La columna first_name almacena el nombre del usuario.
- La columna summary_limit almacena el límite de resúmenes para el usuario con un valor predeterminado de 2 si no se proporciona.
- La columna interactions_count almacena el recuento de interacciones del usuario con un valor predeterminado de 0 si no se proporciona.

```py
CREATE TABLE users (
  user_id BIGINT PRIMARY KEY,
  first_name TEXT,
  summary_limit INT DEFAULT 2,
  interactions_count INT DEFAULT 0
);
```
