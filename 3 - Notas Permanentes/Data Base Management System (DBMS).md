---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Definicion
  - Teoria
---

# Definición

Es un sistema de software de propósito general que facilita los procesos de definición, construcción y manipulación de BD ^hvgbgt

Este tiene una parte de memoria RAM para el mismo.

## Objetivos

- Evitar redundancia e inconsistencia de datos
- Permitir acceso a los datos en todo momento
- Evitar anomalías en el acceso concurrente
- Restricción a accesos no autorizados -> seguridad
- Suministro de almacenamiento persistente de datos (aun ante fallos) -> seguridad desde otra perspectiva
- Integridad en los datos
- Backups

### ¿Qué Hace El DBMS?

Cuando usás SQL (DML), vos le decís **qué** querés obtener o hacer, y el **DBMS (sistema de gestión de base de datos)** se encarga de decidir **cómo** hacerlo de la mejor manera (qué índices usar, qué rutas seguir, etc.).

## Componentes

| Tipo | Lenguaje     | ¿Qué hace?                            | Ejemplos                               |
| ---- | ------------ | ------------------------------------- | -------------------------------------- |
| DDL  | Definición   | Crea la estructura de la BD           | `CREATE`, `ALTER`, `DROP`              |
| DML  | Manipulación | Trabaja con los datos dentro de la BD | `SELECT`, `INSERT`, `DELETE`, `UPDATE` |

### DDL – Data Definition Language (Lenguaje De Definición De Datos)

#### ¿Qué Es?

Es un conjunto de instrucciones del lenguaje SQL que sirven para **definir y estructurar** una base de datos.

#### ¿Qué Cosas Se Hacen Con DDL?

Crear, modificar o borrar:

- **Tablas**
- **Índices**
- **Vistas**
- **Esquemas**
- **Restricciones** (como claves primarias, foráneas, etc.)

> [!example] Ejemplo
>
> ```sql
> CREATE TABLE Clientes (
>     id INT PRIMARY KEY,
>     nombre VARCHAR(100),
>     email VARCHAR(100)
> );
> 
> ALTER TABLE Clientes ADD telefono VARCHAR(20);
> 
> DROP TABLE Clientes;
> ```

#### ¿Qué Genera?

> El resultado de usar DDL es la creación del **Diccionario de Datos**, que es como una “guía técnica interna” del DBMS (Sistema de Gestión de Bases de Datos), donde se guarda:

- Qué tablas hay
- Qué columnas tienen
- Qué tipo de datos aceptan
- Qué restricciones hay
- Qué relaciones hay entre tablas

---

### DML – Data Manipulation Language (Lenguaje De Manipulación De Datos)

#### ¿Qué Es?

Son instrucciones que permiten **interactuar con los datos reales** dentro de las estructuras definidas por el DDL. Se usa para **consultar y modificar** la información.

> [!important] Importante
>
> DML trabaja **dentro** del modelo que definiste con DDL.

#### ¿Qué Hace?

- **Recupera información** (consultas)
- **Agrega** nueva información (<mark class="hltr-r">insertar</mark>[^1] registros)
- **Quita** información (borrar <mark style='background:var(--mk-color-blue)'>registros</mark>)
- **Modifica** información existente (actualizar registros)

> [!example] Ejemplo de Comandos
>
> ```[[SQL]]
> -- Recuperar información
> SELECT * FROM Clientes WHERE nombre = 'Ana';
> 
> -- Agregar información
> INSERT INTO Clientes (id, nombre, email) VALUES (1, 'Ana', 'ana@email.com');
> 
> -- Quitar información
> DELETE FROM Clientes WHERE id = 1;
> 
> -- Modificar información
> UPDATE Clientes SET email = 'nuevo@email.com' WHERE id = 1;
> ```

- Hola
	- Como
		- Estas
	- Todo
Lo mas Importante del DML es
[^1]: Importante
