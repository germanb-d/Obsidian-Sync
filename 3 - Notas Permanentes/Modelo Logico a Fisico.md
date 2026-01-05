---
Categoria: Sistemas
Materia: Base de Datos 1
tags:
---

# Diseño Físico

Relacion Matematica -> Es una tabla de doble entrada

- Fila -> Objetos de la entidad
- Columna -> Atributo
La entidad es una tabla.
La clave se utiliza para que no haya dos filas repetidas.
- **Clave mixta**: Una clave que usa otra entidad para identificar.  No sirve en las tablas.
- Clave Candidata: Cuando tenes varias claves univocas se les llama claves candidatas.
	- En el fisico hay que definir una clave candidata en particular como Clave Primaria

# Modelo Logico a Fisico

Cada entidad es una tabla

Entidad A con atributos X, Y y Z. y Clave compuesta de Y y Z

A = (<u>Y, Z</u>, X)

- Se pone la clave primero y se subraya

## Eliminar Identificadores Externos Y Mixtos

Si tengo claves externas o mixtas debo trasladarlas dentro de la tabla.

Si mi entidad Ciudad tiene una clave Nombre que se relaciona con la entidad Provincia

Ciudad = (<u>nombre, codigo_provincia</u>, X, Y)

![[Drawing 2025-08-25 18.28.23.excalidraw]]

`Persona` = (DNI, Nombre, Apellido)

`Alumno` =

- (<u>Legajo</u>, Promedio, bla bla bla)
- (<u>DNI_Persona</u>, Legajo, Promedio, bla bla bla) yo acá ya sé qué persona es: junto con su nombre y apellido

## Transformar Cada Entidad En Una Relacion

### Cardinalidad Uno a Muchos

![[25-08-25 - lunes-1756158217630.webp]]

Entidad 2 = (identificador entidad 2 + atributos entidad 2)

Entidad 1 = (identificador entidad 1 + atributos entidad 1 + identificador entidad 2 (CF))

- CF: Es una clave foránea, una clave en otra relación
NOTA: En este caso R no es una nueva tabla. Toda fila (o tupla) de la entidad 1, si o si, tiene relación con una sola fila de la entidad 2, lo que nos permite bajar e iIdentificador de la entidad 2 a la entidad 1, transformándose en una clave foránea (que siempre obtendrá algún valor) en la entidad 1.

Pais = (<u>Nombre</u>, Poblacion)

Provincia = (<u>Codigo</u>, nombre, Nombre_pais (CF))

### Cardinalidad Uno a Muchos - Opcional

![[25-08-25 - lunes-1756158417506.webp]]

Lo importante es la cardinalidad (0,1) del lado del 1, cuando esta es opcional hay 2 opciones:

Opción 1 (genera valores nulos, puede no ser conveniente):

- Entidad 2 = (identificador entidad 2 + atributos entidad 2)
- Entidad 1 = (identificador entidad 1 + atributos entidad 1 + identificador entidad 2 (CF))
	- Si la relación tiene un atributo se agrega aca

Opción 2 (solución orientada a tener la menor cantidad de atributos con valores nulos):

- Entidad 2 = (identificador entidad 2 + atributos entidad 2)
- Entidad 1 = (identificador entidad 1 + atributos entidad 1)
- R = (Identificador entidad 1, identificador entidad 2) - Importante: cuál es la clave primaria de esta tabla.
	- Si la relacion tiene un atributo se agrega aca

> [!example] Ejemplo
> Persona = (<u>DNI</u>, nombre, etc)
> O.S. = (<u>NRO</u>, descripcion)
> Prepaga = (<u>DNI</u>, NRO)       (esta es la relacion)

### Cardinalidad Uno a Uno

![[25-08-25 - lunes-1756159370300.webp]]

Opción 1:

- Entidad 2 = (identificador entidad 2 + atributos entidad 2)
- Entidad 1 = (identificador entidad 1 + atributos entidad 1 + identificador entidad 2 (CF))
Opción 2:
- Entidad 2 = (identificador entidad 2 + atributos entidad 2 + identificador entidad 1 (CF))
- Entidad 1 = (identificador entidad 1 + atributos entidad 1)

### Cardinalidad Uno a Uno Opcional

![[25-08-25 - lunes-1756160012518.webp]]

Entidad 2 = (identificador entidad 2 + atributos entidad 2)

Entidad 1 = (identificador entidad 1 + atributos entidad 1)

R = (Identificador entidad 1, identificador entidad 2) - Como clave primaria de esta tabla se podría elegir a identificador entidad 2, pero no ambas al mismo tiempo.

NOTA: En este caso R es una nueva tabla. En el caso de que no transformar a R en una nueva tabla se debería bajar como clave foránea el identificador de entidad 2 a entidad 1 o viceversa. Se intenta evitar claves foráneas nulas.

### Cardinalidad Muchos a Muchos (indistinto Si Es opcional)

![[25-08-25 - lunes-1756160060372.webp|632x110]]

Entidad 2 = (identificador entidad 2 + atributos entidad 2)

Entidad 1 = (identificador entidad 1 + atributos entidad 1)

R = (Identificador entidad 1, identificador entidad 2)

- Son FK aunque no es necesario ponerlo
- En algunos casos las claves se deben ampliar, como en caso de que tenga en la relación `fechaDesde` y `fechaHasta`. Donde `fechaDesde` será una nueva clave para diferenciar épocas.
- Nosotros buscaremos que ambas claves (entidad 1 y 2) sean de entidades existentes. Ej: Si la entidad 1 es `Persona`, busco no poder crear una tabla de relación de un DNI que no existe en la [[Base de Datos]]

![[25-08-25 - lunes-1756160565912.webp|602x387]]

## Relaciones Con Atributos

Cuando las relaciones tienen atributos propios hay 2 opciones:

1) Transformar la relación como hasta ahora según la cardinalidad y opcionalidad.
2) Ubicar los atributos:
a) Si la relación es una nueva tabla: en la nueva tabla (preferido). A veces es necesario agregarle algún atributo de la relación a la clave para hacerla única.
- Ejemplo: En museo y obra donde la relación = (<u>nombre_museo, cod_obra, FD</u>, FH). En este caso, aunque en el modelo lógico la `FechaDesde` no era una clave, acá debe serlo para identificar unívocamente la relación.
b) Si la relación se resuelve con una FK, los atributos de la relación van en la tabla donde está la FK.

## Relaciones N-arias, Recursivas Y Agregaciones

#Revisar  Imagen en el chat de emi

# Identificadores Autoincrementales (ID)

Si yo uso IDs para manejar las claves, aunque son unicas para cada elemento, esto me haria perder que las claves anteriores sean irrepetibles y unicas. El DNI podria repetirse dos veces al no ser una clave. En estos casos deberia aplicar que todas las claves antiguas sean atributos con la propiedad de ser unicos.

Ademas que todas las relaciones que pase a tablas usaran los nuevos IDs como clave.
