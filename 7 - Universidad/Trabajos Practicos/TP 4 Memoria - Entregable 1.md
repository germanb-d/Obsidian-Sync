# Punto 1

# Punto 3

Al trabajar con particiones fijas, los tamaños de las mismas se pueden considerar:

- Particiones de igual tamaño.
- Particiones de diferente tamaño.

## Particiones De Igual Tamaño.

### Ventajas

- Es muy simple de implementar y de administrar
- Como todas las particiones son iguales, se puede asignar cualquier proceso a cualquier partición disponible si cabe.
- No se necesita de ningún criterio de asignación para los procesos, ya que todas las particiones son iguales.

### Desventajas

- Se puede dar que un proceso de menor tamaño ocupe una partición de mayor tamaño, esto **genera una fragmentación interna** (ese espacio sobrante en cada partición).
- Se puede dar que un proceso sea más grande que la partición provocando que este no se puede ejecutar.  Aunque existen soluciones como dividir el proceso en segmentación o paginación, de forma básica sin tomar en cuenta esto se puede interpretar como una desventaja.

## Particiones De Diferente Tamaño

### Ventajas

Podrás tener particiones más grandes en el mismo espacio de memoria de lo que tendrías en una distribución de particiones de igual tamaño, lo cual te **permitirá tener procesos de mayor tamaño**

Además, **aprovecha de mejor forma la memoria** al poder tener procesos de menor tamaño en particiones también de menor tamaño, y así poder reducir la fragmentación interna.

### Desventajas

A diferencia de la distribución igual tamaño, acá si deberás tener un criterio de asignación para cada proceso, para así determinar que partición es mejor para ese proceso. Esto **puede conllevar más tiempo y recursos.**

Aunque en menor medida, **seguirá generando fragmentación interna**.

# Punto 4

Ambos métodos de particiones presentan el problema de la fragmentación:

- Fragmentación Interna (Para el caso de Particiones Fijas)
- Fragmentación Externa (Para el caso de Particiones Dinámicas)

## 1. Explique a Que Hacen Referencia Estos 2 Problemas

La fragmentación interna hace referencia al espacio sobrante que queda al guardar un proceso en una partición fija. Este espacio libre espacio que se desperdicia porque no puede ser usado por otro proceso.

La fragmentación externa hace referencia cuando hay suficiente espacio libre para un proceso, pero este espacio libre está fragmentado en pequeños fragmentos.

![[Administracion de Memoria - Practica Entregable-1747862141372.webp]]

## 2. El Problema De la Fragmentación Externa Es Posible De Subsanar. Explique Una Técnica Que Evite Este Problema.

Se puede subsanar mediante la Compactación, donde el SO reorganiza la memoria para que todos los procesos ocupen un espacio continuo y poder dejar un espacio grande de memoria libre.

# Punto 8

*Ejercicio:* Considere un espacio lógico de 8 páginas de 1024 bytes cada una, mapeadas en una memoria física de 32 marcos

![[Administracion de Memoria.svg]]

## ¿Cuántos Bits Son Necesarios Para Representar Una Dirección Lógica?

La dirección lógica está formada por la **Página + Desplazamiento**

- **Página** = log 2 (8) = 3 bits
	- O sea yo con 3 bits puedo representar todas las páginas, desde la página 0 (000 bin) hasta la página 7 (111 bin)
- **Desplazamiento** = log 2 (32) = 10 bits
	- El desplazamiento puede ir desde 0 hasta 1023, yo puedo representar este tramo con 10 bits, desde la 0 (0000000000 bin) hasta la 1023 (1111111111 bin)

Por lo cual la **Dirección Lógica la puedo representar con 13 bits** = 3 bits de Pág. + 10 bits del desplazamiento

## ¿Cuántos Bits Son Necesarios Para Representar Una Dirección Física?

La Dirección Física está formada por el **Marco + Desplazamiento**

- **Marco** = log 2 (32) = 5 bits
	- Con 5 bits puede representar desde el marco 0 (00000 bin) hasta el marco 32 (11111 bin)
- **Desplazamiento** = 10 bits (es igual que en la DL)

Por lo cual la **Dirección Física la puedo representar con 15 bits** = 5 bits del marco + 10 bits del desplazamiento

# Punto 10

Cite similitudes y diferencias entre la técnica de segmentación y la de particiones dinámicas.

## Similitudes

- En ambos métodos se pueden dar fragmentación externa.
- En ambos usamos bloques de tamaño variable para la memoria
- En ambos podríamos llegar a tener que hacer una compactación
- En ambos se necesita usar una tabla como índice

## Diferencias

- En la segmentación se divide el proceso en distintos segmentos: subrutinas, datos, pilas. En la partición dinámica no.
- La segmentación usa direcciones lógicas de segmento + desplazamiento. La partición dinámica lo hace con la dirección física directamente.
- En la segmentación distintos procesos pueden compartir segmentos. En la partición dinámica no.

# Punto 16

## Tabla De Páginas De 1 Nivel

Es de un solo nivel porque solo ocupa una tabla de páginas lineal.

![[Administracion de Memoria - Practica Entregable-1747862929198.webp]]

Pasar la Dirección Lógica a Dirección Física

- A nosotros nos llega la dirección lógica que sería la **página + desplazamiento**
- Mediante el índice de la tabla vemos a qué marco apunta nuestra página.
- Posteriormente, le sumamos el desplazamiento y así obtenemos la dirección física.

## Tabla De Páginas De Nivel 2

![[Administracion de Memoria - Practica Entregable-1747864557599.webp]]

Es de nivel 2 porque tiene dos tablas:

- La primera tabla de nivel superior: Que apunta a tablas de segundo nivel
- La segunda tabla de segundo nivel: Que apunta a los marcos en la memoria

Pasar la Dirección Lógica a Dirección Física

| 10 Bits | 10 Bits | 12 Bits        |
| ------- | ------- | -------------- |
| TP 1    | TP 2    | Desplazamiento |

Los primeros 10 bits se usan como referencia a la primera tabla

Los segundos 10 bits se usan como referencia a la segunda tabla

Y ya con la dirección en memoria obtenida se le suman los últimos 12 bits de desplazamiento

## Tabla De Páginas Invertida

![[Administracion de Memoria - Practica Entregable-1747865476371.webp]]

Funciona mediante hashing, donde la primera porción se transforma a un valor de hash pasándola por una función de hash. Este valor se busca en la tabla donde se obtiene la información del marco al cual se hace referencia y sumándole el desplazamiento sacamos la dirección física.

# Punto 17

## **1. Tamaño De Página pequeño**

**Ventajas:**

- **Menor fragmentación interna**: Se desperdicia menos espacio dentro de cada página, especialmente si los procesos utilizan poca memoria.
- **Mejor aprovechamiento de la memoria**: Ideal para programas con estructuras de datos pequeñas o acceso disperso a la memoria.
- **Mayor precisión en la carga de datos**: Se pueden traer a memoria solo las partes necesarias del proceso.

**Desventajas:**

- **Mayor tamaño de la tabla de páginas**: Más páginas implican más entradas en la tabla de páginas, lo que consume más memoria y puede requerir más accesos a memoria.
- **Mayor sobrecarga de administración**: El sistema operativo debe gestionar más páginas, lo cual puede aumentar el costo de conmutación de contexto y paginación.

## **2. Tamaño De Página grande** #IA

**Ventajas:**

- **Menor tamaño de la tabla de páginas**: Al haber menos páginas, la tabla de páginas es más pequeña, lo que reduce el uso de memoria y mejora el acceso.
- **Menor sobrecarga de administración**: Menos páginas que gestionar, menos interrupciones por fallos de página.
- **Eficiencia en transferencias**: Las operaciones de E/S (lectura/escritura) entre disco y memoria son más rápidas porque se transfieren bloques más grandes.

**Desventajas:**

- **Mayor fragmentación interna**: Si el proceso no utiliza toda la página, se desperdicia más espacio.
- **Uso ineficiente de memoria**: No es óptimo para procesos con acceso disperso o con pequeños requerimientos de memoria.
- **Carga innecesaria de datos**: Se pueden cargar partes del programa que no se usan, ocupando espacio en RAM sin necesidad.

# Punto 18

Asignación de marcos a un proceso (Conjunto de trabajo o Working Set):

Con la memoria virtual paginada, no se requiere que todas las páginas de un proceso se encuentren en memoria. El SO debe controlar cuantas páginas de un proceso puede tener en la memoria principal. Existen 2 políticas que se pueden utilizar:

- Asignación Fija
- Asignación Dinámica.

1. Preguntas
	1. Describa cómo trabajan estas 2 políticas.
	2. Dada la siguiente tabla de procesos y las páginas que ellos ocupan, y teniéndose 40 marcos en la memoria principal, cuántos marcos le corresponden a cada proceso si se usa la técnica de Asignación Fija:
		1. Reparto Equitativo
		2. Reparto Proporcional

| Proceso | Total de Paginas Usadas |
|:-------:|:-----------------------:|
|    1    |           15            |
|    2    |           20            |
|    3    |           20            |
|    4    |            8            |

La **asignación de marcos de página** a procesos en un sistema de **memoria virtual paginada** es crucial para el rendimiento y la estabilidad del sistema. Las dos políticas principales son:

---

## Asignación Fija

### ✅ Características:

- Cada proceso recibe una **cantidad fija de marcos** en memoria principal, determinada al momento de su carga o mediante una política previa (como proporcional al tamaño del proceso).
- Esta cantidad **no cambia** durante la ejecución del proceso.

### 👍 Ventajas:

- **Simplicidad** en la implementación.
- **Predecible**: el sistema sabe cuántos marcos necesita reservar para cada proceso.

### 👎 Desventajas:

- **Desperdicio de memoria** si un proceso no necesita tantos marcos.
- **Thrashing** (exceso de paginación) si el número de marcos asignados no es suficiente para su conjunto de trabajo.
- **Inflexibilidad**: no se adapta al comportamiento cambiante del proceso.

## 📌 **2. Asignación Dinámica (Conjunto De Trabajo / Working Set)**

### ✅ Características:

- El número de marcos asignados a un proceso puede **variar durante la ejecución**, según sus necesidades actuales.
- Se basa en la noción de **conjunto de trabajo**, que es el conjunto de páginas que un proceso ha utilizado recientemente (dentro de una ventana de tiempo definida).

### 👍 Ventajas:

- **Mejor uso de memoria**: se asignan marcos según necesidad real.
- **Reducción del thrashing**: los procesos tienen suficiente memoria para ejecutar eficientemente.
- **Adaptabilidad**: se ajusta al comportamiento del proceso en tiempo real.

### 👎 Desventajas:

- **Mayor complejidad** en la implementación.
- **Sobrecarga del sistema operativo** para monitorear el conjunto de trabajo y ajustar asignaciones.
- Riesgo de **interferencia entre procesos** si hay poca memoria disponible.

---

<mark style='background:var(--mk-color-yellow)'>El resto esta en el cuadernillo</mark>

# Punto 19
