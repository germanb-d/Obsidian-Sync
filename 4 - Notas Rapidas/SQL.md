# Introduccion

Structured Query Language - Lenguaje de consulta estructurado

Lenguaje declarativo de acceso a bases de datos relacionales que permite especificar diversos tipos de operaciones sobre las mismas.

Es el lenguaje estandarizado para consultas en base de datos. Aunque muchos sistemas traen opciones extras, aca buscaremos desarrollar SQL base.

## MySQL

### Tipos De Datos

- Numéricos: `INTEGER`, `SMALLINT`, `DECIMAL`, `FLOAT`.
- Fecha: `DATE`, `DATETIME`, `TIME`.
	- Cadena de caracteres: `CHAR(N)`, `VARCHAR(N)`, `TEXT`, `MEMO`.
	- `CHAR (N)`: Donde N es un numero fijo
	  `VARCHAR (N)`: Longitud Variable `[!!info|No usar si sabemos que el campo es fijo|var(--color-red-rgb)]`
- Cadenas binarias: `BINARY`, `BLOB`.

> [!note]
> No existe el tipo BOOLEAN.

#### NULL

Es compatible con cualquier tipo, NULL puede indicar: No aplicable, Desconocido.

Para preguntar si un valor es Null, generalmente se provee la forma especial IS NULL o IS NOT NULL (en vez de = Null o <> Null)

# Comandos

## DDL

No se toma muy a fondo porque,  usualmente, se utiliza una GUI para hacerlo y no por codigo.

Comandos:

- CREATE
- DROP
- ALTER

Se utiliza para las exportaciones en tipo DDL y para cuando alguna herramienta grafica no funcione igualmente se puede utilizar DDL.

## DML

- SELECT (consultar)
- INSERT
- DELETE
- UPDATE

```SQL
SELECT lista de expresiones TOP n 6 
FROM lista de tablas 1
WHERE lista de condiciones 2
GROUP BY lista de campos de agrupamiento 3
HAVING lista de condicones que deben cumplir los grupos 4
ORDER BY lista de criterios de ordenamiento 5
UNION ALL
```

Se dice expresiones porque en las columnas puede haber funciones complejas.
