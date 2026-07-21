-----
###### Tags: #vulnerabilidad #web #basededatos 

------------------------------------------------------
# TEORIA

> **SQL Injection (SQLi)** es una vulnerabilidad de seguridad que permite a un atacante modificar o inyectar consultas SQL mediante entradas controladas por el usuario. Si la aplicación no valida o parametriza correctamente los datos recibidos, el atacante puede consultar, modificar o eliminar información almacenada en la base de datos, e incluso llegar a comprometer completamente el servidor en determinados escenarios.

-----------
## ¿Cómo funciona?

Una aplicación vulnerable concatena directamente el input del usuario dentro de una consulta SQL.

Por ejemplo:

```SQL
SELECT * FROM users WHERE username = '$username' AND password = '$password';
```

Si el usuario introduce caracteres especiales o consultas SQL, estos serán interpretados por el motor de base de datos.

-----------
## Tipos

- **I

-----------
## ¿Cómo se explota?

1. 

-----------
## Payloads comunes
### Bypass de Login

```SQL
' OR 1=1--
```

### UNION

```SQL
UNION SELECT NULL,NULL,NULL--
```

### UNION

```SQL
UNION SELECT NULL,NULL,NULL--
```

-----------
## Funciones útiles

### MySQL
-

### PostgreSQL
-

### Microsoft SQL Server
-

### Oracle
-

-----------
## ¿Donde explotar esta vulnerabilidad?

- Parámetros GET
- Parámetros POST
- Cookies
- Headers HTTP

-----------

## Herramientas que lo usan

- [[SQLMap]]
- [[Burp Suite]]

-----------
## Prevención

- Consultas preparadas (Prepared Statements)
- Parametrización de consultas
- ORM
- Validación de entradas
- Manejo de errores
- WAF

-----------
## Referencias

- https://owasp.org/www-community/attacks/SQL_Injection
- https://portswigger.net/web-security/sql-injection
- https://cheatsheetseries.owasp.org/