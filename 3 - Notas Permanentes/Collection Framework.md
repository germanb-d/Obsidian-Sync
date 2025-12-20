---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

![[collection-frameworks-lesson-8.pdf]]

# Que Es

Es una [[API]] que utiliza java para el manejo de [[Colecciones]].  Es una arquitectura unificada para administrar colecciones

## Partes Principales Del Framework:

- **Interfaces**
	- Definen la funcionalidad común entre las colecciones
- **Implementaciones**
	- Clases concretas las cuales proporcionan las estructuras de datos
- **Operaciones (algoritmos)**
	- Métodos que realizan diversas operaciones sobre las colecciones.

## Funciones Principales

- Agregar objetos a una colección
- Quitar objetos de la colección
- Encontrar un objeto o un grupo de objetos en una colección
- Recuperar un objeto de una colección (sin quitarlo de la colección)
- Iterar a través de una colección, viendo cada elemento, uno después de otro.

# Jerarquía Del Framework

Dentro del Framework de Collections se pueden distinguir **dos grupos principales** de interfaces:

## Grupo Collection

- **Collection** (interfaz raíz)
  - **Set** → No permite duplicados
  - **List** → Permite duplicados y usa índices

![[collection-frameworks-lesson-8.pdf#page=12&rect=50,28,783,409|collection-frameworks-lesson-8, p.12]]

### Set

#### Definición

**Set** es una interfaz que representa una colección de elementos **únicos** (sin duplicados). Se basa en el concepto matemático de conjunto.

#### Características Principales

**Sin duplicados**
- No permite elementos repetidos
- Utiliza `{java}equals()` para determinar si dos objetos son iguales
  
**Sin orden específico**
- Un Set básico no mantiene un orden particular de elementos
- (Excepción: algunas implementaciones sí mantienen orden)
  
**Hereda de Collection**
- Tiene exactamente los mismos métodos que Collection
- Pero añade la restricción de unicidad

#### Implementaciones Principales

| Implementación    | Características                                                                                 |
| ----------------- | ----------------------------------------------------------------------------------------------- |
| **HashSet**       | • Mejor performance<br>• Almacena en tabla de hash<br>• No mantiene orden                       |
| **LinkedHashSet** | • Versión ordenada de HashSet<br>• Mantiene orden de inserción                                  |
| **TreeSet**       | • Elementos ordenados naturalmente<br>• Implementa SortedSet<br>• Requiere elementos Comparable |

##### Caso De Uso Típico:

Eliminar duplicados de una colección:

```Java
Set<String> sinDup = new TreeSet<String>(coleccionConDuplicados);
```

### List

#### Definición

**List** es una interfaz que representa una colección **ordenada** de elementos que **permite duplicados**. Los elementos se organizan por **posición** o **índice**.

#### Características Principales

 **Basada en índices**
- Cada elemento tiene una posición numérica (0, 1, 2, ...)
- Acceso directo por índice

**Permite duplicados**
- Puede contener el mismo objeto múltiples veces
- No hay restricción de unicidad

**Mantiene orden**
- Los elementos están ordenados por posición
- El orden se mantiene según inserción o manipulación

**Hereda de Collection**
- Incluye todos los métodos básicos de Collection
- Añade métodos específicos para trabajo con índices

#### Implementaciones Principales

| Implementación | Características                                                                                   |
| -------------- | ------------------------------------------------------------------------------------------------- |
| **ArrayList**  | • Acceso aleatorio rápido<br>• Basado en array dinámico<br>• Mejor para lectura                   |
| **LinkedList** | • Inserciones/eliminaciones rápidas<br>• Lista doblemente enlazada<br>• Mejor para modificaciones |
| **Vector**     | • Versión sincronizada de ArrayList<br>• Thread-safe<br>• Menos usado actualmente                 |

#### Métodos Específicos De List

```java
E get(int index)                    // Obtener elemento por índice
int indexOf(E element)              // Encontrar índice de elemento
int lastIndexOf(E element)          // Último índice de elemento
E remove(int index)                 // Remover por índice
E set(int index, E element)         // Reemplazar en posición
boolean add(int index, E element)   // Insertar en posición
```

##### Funcionalidades Adicionales:

- **Algoritmos**: `sort()`, `shuffle()`, `reverse()`, `replaceAll()`
- **Sublistas**: `subList(fromIndex, toIndex)` para trabajar con rangos

##### Caso De Uso Típico:

Cuando necesitas mantener orden y acceder por posición:

```java
List<String> nombres = new ArrayList<>();
nombres.add("Juan");
nombres.add("María");  
nombres.add("Juan");  // Duplicado permitido
System.out.println(nombres.get(0)); // "Juan"
```

## Grupo Map

- **Map** → Maneja pares (clave-valor)
  - **SortedMap** → Map con claves ordenadas
![[collection-frameworks-lesson-8.pdf#page=13&rect=175,3,719,428|collection-frameworks-lesson-8, p.13]]

### Map

#### Definición:

**Map** es una interfaz que almacena elementos como **pares clave-valor** (duplas). Mapea una **clave única** a un **valor específico**. Tanto clave como valor son objetos.

#### Características Principales:

**Pares clave-valor**
- Cada elemento es una dupla (K, V)
- La clave actúa como identificador único
- Un valor puede estar asociado a múltiples claves

**Claves únicas**
- No puede haber claves duplicadas
- Si se inserta una clave existente, se reemplaza el valor

**No Hereda De Collection**
- Es una jerarquía completamente separada
- No es una "colección" en el sentido tradicional

**Búsqueda eficiente**
- Permite buscar valores rápidamente usando la clave
- Utiliza `hashCode()` y `equals()` para gestionar claves

#### Métodos Específicos De Map (buscado En GPT)

```java
V put(K key, V value)           // Insertar/actualizar par clave-valor
V get(Object key)               // Obtener valor por clave
V remove(Object key)            // Remover por clave
boolean containsKey(Object key) // Verificar si existe la clave
boolean containsValue(Object value) // Verificar si existe el valor
Set<K> keySet()                 // Obtener conjunto de claves
Collection<V> values()          // Obtener colección de valores
```

#### Implementaciones Principales:

| Implementación    | Características                                                                           |
| ----------------- | ----------------------------------------------------------------------------------------- |
| **HashMap**       | • Mejor performance general<br>• Usa hashcode para localizar<br>• No mantiene orden       |
| **LinkedHashMap** | • Mantiene orden de inserción<br>• Más lento que HashMap<br>• Predecible al iterar        |
| **TreeMap**       | • Elementos ordenados por clave<br>• Implementa SortedMap<br>• Requiere claves Comparable |

#### Casos De Uso Típicos:

- **Diccionarios**: palabra → definición
- **Catálogos**: código → producto
- **Cachés**: ID → objeto
- **Configuraciones**: parámetro → valor

#### Ejemplo:

```java
Map<String, Integer> edades = new HashMap<>();
edades.put("Juan", 25);
edades.put("María", 30);
System.out.println(edades.get("Juan")); // 25
```

#### Nota Importante:

El método `hashCode()` debe ser sobrescrito correctamente para que las claves funcionen como identificadores únicos.
