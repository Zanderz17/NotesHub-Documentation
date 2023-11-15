---
sidebar_position: 4
---

# Utils_db

## save_user(user_id, first_name, summary_limit=None)

Esta función guarda o actualiza la información del usuario en la base de datos PostgreSQL.

1. Conecta con la base de datos PostgreSQL utilizando los parámetros de conexión proporcionados.
2. Intenta insertar un nuevo registro o actualizar uno existente en la tabla users.
3. La actualización se realiza basándose en el user_id.
4. Si summary_limit se proporciona, actualiza el valor del límite de resúmenes; de lo contrario, usa el valor predeterminado de 2.
5. Confirma la transacción y cierra la conexión.

### Uso

```py
save_user(123456, "John Doe", 5)
```

## get_summary_limit(user_id)

Esta función obtiene el límite de resúmenes permitidos para un usuario específico desde la base de datos.

1. Conecta con la base de datos PostgreSQL utilizando los parámetros de conexión proporcionados.
2. Consulta el límite de resúmenes para el usuario específico en la tabla users.
3. Retorna el límite si se encuentra; de lo contrario, retorna None.
4. Cierra la conexión.

### Uso

```py
limit = get_summary_limit(123456)
```

## is_summary_limit_positive(user_id)

Esta función verifica si el límite de resúmenes para un usuario es mayor que cero.

1. Conecta con la base de datos PostgreSQL utilizando los parámetros de conexión proporcionados.
2. Consulta el límite de resúmenes para el usuario específico en la tabla users.
3. Retorna True si el límite es mayor que cero, False de lo contrario.
4. Cierra la conexión.

### Uso

```py
result = is_summary_limit_positive(123456)
```

## decrease_summary_limit(user_id)

Esta función disminuye en 1 el valor del límite de resúmenes para un usuario.

1. Conecta con la base de datos PostgreSQL utilizando los parámetros de conexión proporcionados.
2. Intenta disminuir en 1 el valor del límite de resúmenes para el usuario en la tabla users.
3. Confirma la transacción y cierra la conexión.

```py
decrease_summary_limit(123456)
```

## increment_interactions_count(user_id)

Esta función incrementa en 1 el valor de interactions_count para un usuario.

1. Conecta con la base de datos PostgreSQL utilizando los parámetros de conexión proporcionados.
2. Incrementa en 1 el valor de interactions_count para el usuario en la tabla users.
3. Confirma la transacción y cierra la conexión.

```py
increment_interactions_count(123456)
```

## Notas Adicionales:

- Asegúrese de tener instalada la biblioteca psycopg2 para el correcto funcionamiento de estas funciones.
- Los parámetros de conexión a la base de datos se obtienen de las variables de entorno cargadas mediante load_dotenv(). Asegúrese de tener estas variables de entorno configuradas.
