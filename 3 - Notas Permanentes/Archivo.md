---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Definicion
  - Teoria
---

# Definiciones

## Conceptual

 Un archivo es una estructura de datos que recopila una colección de registros semejantes en un dispositivo de almacenamiento secundario.

## Práctica En [[Base de Datos]]

Unidad lógica de almacenamiento permanente de [[Registro|registros]], administrada por un Sistema Operativo. Dentro de un archivo, los registros pueden organizarse en otras unidades lógicas (unidades de organización) llamadas bloques.

**Es una estructura de datos homogénea**
<center></center>

# Tipos De Archivos

![[Archivos-1751309697273.webp]]

**Secuencia de bytes**: Archivos de texto, no se puede determinar fácilmente comienzo y fin de cada dato

**Registros**: conjunto de campos agrupados que definen un elemento del archivo
**Campos**: unidad más pequeña, lógicamente significativa, de un archivo.

O sea, un Archivo contiene Registros, el cual está compuesto por un conjunto de Campos.

> [!question] Que tiene el Campo dentro? No es una secuencia de bytes?
> No, la diferencia es q el campo contiene un tipo de dato definido. A diferencia de en un `.txt` donde es texto plano (no se distingue el tipo)

## Tipos De Archivos Según Volatilidad

**Estáticos** -> Pocos cambios
- Puede actualizarse en procesamientos por lotes
- No necesita estructuras adicionales para agilizar los cambios

**Volátiles** -> Sometidos a operaciones frecuentes

Agregar / Borrar / Actualizar

- Su organización debe facilitar cambios rápidos
- Necesita estructuras adicionales para mejorar los tiempos de acceso

## Estructura Jerárquica De Almacenamiento En Archivos

```
Archivo
    └── Registros
            └── Campos
```

| <center>Elemento</center> | <center>Función</center>                    |
| ------------------------- | ------------------------------------------- |
| Archivo                   | Contenedor general                          |
| [[Bloque]]                | Unidad de acceso físico y agrupación lógica |
| [[Registro]]              | Datos relacionados (una fila)               |
| [[Campo]]                 | Dato individual (una celda)                 |

> [!important] Importante
> ![[Bloque]]

# Archivo Físico Y Lógico

## Archivo Físico

Es el archivo **real y tangible** que está guardado en el **almacenamiento secundario** (disco duro, SSD, etc.).

Un archivo `ventas2025.dat` que está en `C:\Datos` y que ocupa 2 MB.

## Archivo Lógico

> Es **una representación abstracta del archivo** dentro del **programa o sistema** que lo utiliza.

Lo **usa un programa** (como una base de datos, o un lenguaje de programación como C o Java) para trabajar **sin preocuparse de los detalles físicos** del archivo.

- Es como un **puente o interfaz** entre el programa y el archivo físico.
- Permite hacer operaciones como `abrir`, `leer`, `escribir`, `cerrar`, etc., sin saber el nombre físico exacto ni su ubicación.
- Se puede redirigir a distintos archivos físicos según se necesite.

> [!example] Codigo C
>
> ``` C
> FILE *archivoVentas;
> ArchivoVentas = fopen ("ventas 2025. Dat", "r");
> 
> ```
>
> Acá, `archivoVentas` es el **archivo lógico** que apunta al archivo físico `"ventas2025.dat"`.

# Características

## Acceso a Archivos

- **Secuencial**: Acceso a los registros uno tras otro y en el orden físico en el que están guardados
- **Secuencial indizado**: Acceso a los registros de acuerdo al orden establecido por otra estructura. (Ej: índice temático de un libro)
- **Directo:** Se accede a un registro determinado sin necesidad de haber accedido a otro registro previamente

## Organización De Archivos

Cómo se almacenan y acceden los registros (datos) dentro de un archivo en un sistema.

Como se almacenan, eliminan, modifican y se consulta su contenido.

### Operaciones Primitivas

- **Creación**: creación y carga inicial sin validación de unicidad ni verificación de espacio libre.
- **Actualización de Registros**: inserción con validación de unicidad y aprovechamiento de espacio libre, modificación, y supresión con administración de espacio libre.
- **Recuperación de Registros**: consulta o recuperación unitaria de registros, y reporte o recuperación comprensiva.
- **Mantenimiento**: reestructuración (reconstrucción), depuración y respaldo.

### Modos De Acceso

#### Secuencial

Se recorren los registros **uno a uno** desde el inicio hasta el final.

Pero a veces puede usarse **acceso relativo** si se quiere llegar rápidamente a una posición conocida (por ejemplo, el registro n.º 25 directamente).

##### La Forma De Organizar Los Registros Depende De Su Longitud

###### Registros Son De Longitud Fija:

- Cada registro ocupa el mismo espacio.
- Es fácil calcular la posición de un registro, por ejemplo:  
    `posición = número_de_registro × tamaño_del_registro`

###### Registros Son De Longitud Variable:

- **No actualizables**:
    - Se pueden almacenar **uno detrás de otro directamente** (como un texto continuo), sin bloques.
- **Actualizables**:
    - Se organizan en **bloques**, dejando espacio extra para posibles modificaciones.
    - Esto permite que si un registro cambia de tamaño, no sea necesario mover todo el archivo.

##### Las Primitivas (operaciones) Varían Según El Tipo De Archivo

###### Registros Ordenados Por Identificador (clave):

- Se pueden usar técnicas como **búsqueda binaria** (más eficiente).
- Las **altas** (nuevos registros) pueden requerir **insertar en el medio** y reorganizar.

###### Registros Desordenados:

- Las búsquedas son **más lentas** (requieren recorrer todo).
- Pero es más fácil insertar (solo se agrega al final).

###### Si El Archivo no Requiere Actualizaciones:

- Solo se realizan **altas al final del archivo**.
- Es típico en **archivos transaccionales**, donde se guarda el historial y no se modifica lo pasado.

#### Secuencial Indizado

> Es un método donde los **registros se almacenan en forma secuencial**, pero se utiliza un **índice** para facilitar el acceso directo a determinados grupos de registros.

1. Los **registros están ordenados** por una [[Registro#Clave|clave]] (por ejemplo, DNI).
2. Se crea un **índice** que guarda las claves de algunos registros (no todos), y su posición en el archivo.
3. Para buscar un registro:
    - Primero se consulta el **índice** (rápido).
    - Luego se accede **secuencialmente** desde esa posición hasta encontrar el registro buscado.

#### Relativo / Directo

Se accede directamente al registro mediante el [[NRR]].
