---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Teoria
  - Definicion
---

# ¿Qué Es Un Registro?

Un **registro** es una **unidad lógica de almacenamiento de datos** dentro de un [[Archivo]].  
Contiene un conjunto de [[Campo|campos]] relacionados entre sí, que representan una **entidad completa** (por ejemplo, un alumno, un producto, un paciente).

# ¿Para Qué Sirve?

- Para organizar la información de forma estructurada.
- Es la base de archivos, tablas de bases de datos, etc.
- Permite acceder, modificar o eliminar datos específicos fácilmente.

> [!example] Ejemplo
>
> |Campo|Valor|
> |---|---|
> |Nombre|"Lucía"|
> |Edad|20|
> |Legajo|12345|

# Clave

Es un **campo (o conjunto de campos)** dentro de un registro que **identifica de forma única** (en caso de ser clave primaria) a ese registro dentro del archivo o la tabla.

> [!example] Ejemplo
> - DNI en un archivo de personas.
> - Número de cuenta en un archivo bancario.
> - Legajo en un archivo de alumnos.

**Clave primaria** = identidad única de un registro.  
**Clave secundaria** = criterio alternativo para buscar, pero no garantiza unicidad.

| <center>Característica</center> | <center>**Clave primaria**</center>              | <center>**Clave secundaria**</center>                                          |
| ------------------------------- | ------------------------------------------------ | ------------------------------------------------------------------------------ |
| **Propósito**                   | Identifica **unívocamente** a cada registro.     | Se usa para **buscar o agrupar** registros, pero no identifica de forma única. |
| **Valor**                       | **Único y no nulo** para cada registro.          | **Puede repetirse** y puede ser nulo.                                          |
| **Existencia**                  | Siempre debe existir.                            | Es opcional.                                                                   |
| **Ejemplo clásico**             | DNI, número de cuenta, matrícula, legajo.        | Localidad, profesión, edad, etc.                                               |
| **Índice**                      | Normalmente se usa para el **índice principal**. | Se usa para **índices secundarios**.                                           |
| **Relación**                    | Cada registro tiene **una sola clave primaria**. | Puede tener **una o más claves secundarias**.                                  |

# Tipos De Registro

## Longitud Fija / Predecible

Todos los registros ocupan el mismo espacio.

**Estructura:** Cada campo tiene un tamaño fijo asignado previamente. Por ejemplo, si definimos un campo "nombre" de 50 caracteres, siempre ocupará 50 bytes, incluso si el nombre real solo tiene 10 caracteres.

```
Registro de empleado (longitud fija):
- ID: 10 caracteres
- Nombre: 50 caracteres  
- Apellido: 50 caracteres
- Teléfono: 15 caracteres
Total por registro: 125 bytes
```

### Ventajas Y Desventajas

**Ventajas:**

- **Acceso directo rápido**: Es fácil calcular la posición exacta de cualquier registro multiplicando el número de registro por el tamaño fijo del registro
- **Simplicidad de implementación**: La gestión de memoria y el acceso a los datos es más sencillo
- **Mejor rendimiento en operaciones de búsqueda**: Las operaciones de indexación y búsqueda son más eficientes
- **Facilita la implementación de algoritmos**: Los algoritmos de ordenamiento y búsqueda son más directos

**Desventajas:**

- **Desperdicio de espacio**: Si los datos reales son menores al tamaño asignado, se malgasta espacio de almacenamiento
- **Limitación de tamaño**: Los campos no pueden exceder el tamaño predefinido
- **Inflexibilidad**: Cambiar el tamaño de un campo requiere reestructurar toda la base de datos

---

## Longitud Variable

El tamaño varía según el contenido de los campos.

### En Qué Casos Querría Usar Longitud Variable

``` c
Type Empleado = Record;
        Nombre : string[50];
        Dirección : string[50];
        Documento : string[12];
        Edad : integer;
        Observaciones : string[200];
    End;

```

El registro anterior ocupa 314 bytes. Cada vez que se ingresan los datos de un empleado, en promedio se ocupan 30 lugares para el nombre, otro tanto para la dirección y, en algunos casos, 50 bytes para observaciones. En promedio, cada registro utiliza 124 de los 314 bytes disponibles. Esto significa desperdicio de espacio y mayor tiempo de procesamiento. Se transfieren 314 bytes, de los cuales solo 124 representan información útil; el resto son espacios de relleno.

### Como Sé El Tamaño

**Indicador de longitud** -> Registro comienza con tamaño del registro

**Delimitador** -> Carácter especial para separar registros

**Segundo archivo** -> Archivo que guarda direcciones de registros

### Ventajas Y Desventajas

**Ventajas:**

- **Eficiencia de espacio**: Solo se usa el espacio necesario para los datos reales
- **Flexibilidad**: Los campos pueden crecer o decrecer según sea necesario
- **Mejor para datos heterogéneos**: Ideal cuando los datos varían significativamente en tamaño

**Desventajas:**

- **Complejidad de acceso**: Calcular la posición de un registro específico requiere leer todos los registros anteriores, si no se dispone de un índice.
- **Necesita información adicional**:
	- Registro Fijo:  `"Juan    Pérez   25"  (15 bytes de datos puros)`
	- Registro Variable:  `"04Juan05Pérez0225" (15b de datos + 6b de metadatos = 21 bytes)`
- **Mayor complejidad de implementación**: Requiere algoritmos más complejos.
- Fragmentación: Puede haber [[Fragmentación#Fragmentación Externa|fragmentación externa]] del espacio de almacenamiento.
-  **Rendimiento más lento**: Las operaciones de búsqueda y la actualización de registros son más complejas. Por ej.: Para actualizar un registro en registros fijos solo sobrescribes el mismo lugar, con registros variables: Necesitas:
	- 1. Marcar el espacio viejo como libre
	- 2. Encontrar un nuevo espacio del nuevo tamaño del registro en caso de no entrar en el espacio viejo (fragmentación externa)
	- 3. Actualizar todos los índices
	- 4. Posible reorganización del archivo
