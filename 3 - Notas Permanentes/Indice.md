---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Definicion
  - Teoria
---

# Definición

Estructura de datos (clave, dirección) usada para encontrar [[Registro|registros]] en un [[Archivo|archivo]]. Consiste de un [[Campo]] de llave (búsqueda) y un [[Campo]] de referencia que indica donde encontrar el [[Registro]] dentro del [[Archivo]] de datos. (Es necesario que las claves permanezcan ordenadas).

(clave, [[NRR]] /distancia en bytes)

Este índice en un [[Archivo]] con registros de longitud fija (independientemente si el [[Archivo]] original también lo es). La ventaja es que permite que haya un orden en el [[Archivo]] sin modificarlo.

El índice se puede crear a partir de la [[Registro#Clave|clave]] primaria, y se denomina índice primario. El índice está ordenado por la clave primaria. y es posible aplicar búsqueda binaria, ya que es un [[Archivo]] de longitud fija.

En resumen, usando un índice, se busca en este (puede ser binaria o secuencial) y luego se realiza una única lectura al [[Archivo]] con datos.

## Operaciones Básicas

**Creación** -> Al comienzo se crean los dos archivos vacíos.

**Altas** -> Al realizar un alta, el nuevo [[Registro]] se agrega al final del [[Archivo]] de datos, y usando ese [[NRR]] y la clave, se almacena de forma ordenada en el índice.

**Modificación** -> La única parte que no se puede modificar es la clave, ya que al modificarla no quedaría ordenada en el índice. Si el [[Archivo]] de datos es de longitud fija el índice no se modifica, en cambio, si es de longitud variable puede ser necesario modificar el [[NRR]] en el índice, ya que se reubicaría en el [[Archivo]] de datos.

**Bajas** -> Se busca en el índice para dar de baja tanto en el [[Archivo]] de datos como en el índice. Las bajas lógicas en el índice no se pueden aprovechar con las nuevas altas, ya que esto alteraría el orden del índice.

## Índices Secundarios

Una **clave secundaria** es un [[Campo]] que **puede repetirse** y se usa para buscar registros de forma **más intuitiva** (como el título de una canción).  
Se crea un **índice secundario** que **relaciona cada clave secundaria con una o más claves primarias**.

El proceso de búsqueda es:

1. Buscar por **clave secundaria** (dato fácil de recordar).
2. Obtener la **clave primaria** correspondiente.
3. Buscar el [[Registro]] en el índice primario con la clave primaria.
4. El índice primario da la dirección del [[Registro]].

### Operaciones Básicas De Índices Secundarios

**Creación** -> Se crean todos los índices secundarios necesarios junto con el [[Archivo]] de datos y el índice primario.

**Altas** -> Las altas en el [[Archivo]] primario también generan un alta en el índice secundario. Además, esta alta implica reacomodar el [[Archivo]] con base en la clave secundaria e incluso puede haber un segundo orden de ordenación basándonos en la clave primaria.

**Modificaciones** -> Si se modifica la clave secundaria, se tiene que reacomodar el índice secundario, si se modifica cualquier otro [[Campo]] (excepto la clave primaria), el índice secundario no sufre cambios.

**Bajas** -> Hay dos opciones, se puede eliminar del [[Archivo]] secundario y del índice primario, o solo del índice primario, y que este actúe como una barrera para el secundario. La desventaja es que si el [[Archivo]] es muy volátil, se deberían programar bajas físicas cada tanto en el índice secundario, para que no crezca demasiado.

## Índices Selectivos

- Contienen llaves solo para una porción de los registros del [[Archivo]] de datos que interesa acceder  Ej. Solo contenga los títulos de música clásica
- Vemos solo un subconjunto de los registros del [[Archivo]]

# Ventajas Y Desventajas

## Ventajas

### Mejora Dramática En la Velocidad De Consultas

**Búsquedas más rápidas:**
- Sin índice: Búsqueda secuencial O(n) - examina cada [[Registro]]
- Con índice: Búsqueda logarítmica O(log n) - examina solo algunos registros

### Optimización De Operaciones De Ordenamiento

**ORDER BY más eficiente:**
- Sin índice: ordenamiento completo de todos los registros O(n log n)
- Con índice: los datos ya están ordenados en el índice O(1)

### Optimización De Consultas Y Operaciones De Rango

**Agrupaciones más eficientes:**
- Los datos ya están agrupados lógicamente en el índice
- Reduce significativamente el tiempo de procesamiento

### Garantía De Unicidad

**Índices únicos:**
- Impiden duplicados automáticamente
- Mantienen la integridad de datos sin verificaciones adicionales

## Desventajas

### Overhead De Almacenamiento

**Espacio adicional significativo:**
- Cada índice puede ocupar del 10% al 50% del tamaño de la tabla original
- Múltiples índices pueden duplicar o triplicar el espacio necesario

### 2. Degradación Del Rendimiento En Escrituras

**Operaciones INSERT, UPDATE, DELETE más lentas:**

**INSERT:**
- Insertar el [[Registro]] en la tabla
- Actualizar TODOS los índices existentes
- Mantener el orden en cada índice

**UPDATE:**
- Si se modifica un [[Campo]] indexado, hay que reordenar el índice
- Puede requerir mover entradas a diferentes posiciones

**DELETE:**
- Eliminar el [[Registro]] de la tabla
- Eliminar la entrada de TODOS los índices
- Reorganizar los índices si es necesario

### Costo De Mantenimiento

**Actualizaciones constantes:**
- Los índices deben mantenerse sincronizados con los datos
- Reorganización periódica para mantener eficiencia
- Análisis de estadísticas para el optimizador

**[[Fragmentación]] de índices:**
- Con el tiempo, los índices se fragmentan
- Requieren reconstrucción periódica
- Proceso costoso en términos de recursos
