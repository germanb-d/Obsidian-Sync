---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - Teoria
  - BaseDeDatos
---

# Definición De Árboles Como Índices

Los árboles como [[Indice|índices]] son estructuras de datos jerárquicas que organizan las [[Registro#Clave|claves]] de búsqueda en forma de árbol, donde cada nodo contiene una o más claves y referencias a otros nodos o a los datos reales. Esta organización permite búsquedas, inserciones y eliminaciones eficientes sin necesidad de mantener un orden lineal estricto.

# Solución a Los Problemas De Índices Tradicionales

## 1. Problema: Índices Grandes En Memoria Secundaria

**Solución con árboles:**
- Los árboles se diseñan para minimizar la altura
- Estructura jerárquica permite acceso selectivo a partes del índice
- Solo se cargan en memoria los nodos necesarios para la búsqueda

Ejemplo visual de un Árbol B:

```
Nivel 0 (Raíz):     [50|100|150]
                   /    |    |    \
Nivel 1:      [25|35] [75|80] [125|130] [175|200]
             /  |  |   |   |    |    |    |    |
Nivel 2:   [10][30][40][70][85][120][135][170][190]
```

```
Paso 1: Cargar solo el nodo raíz
Memoria: [50|100|150] (12 bytes)
Decisión: 85 < 100, ir al hijo del medio

Paso 2: Cargar solo el nodo [75|80]
Memoria: [50|100|150] + [75|80] (20 bytes total)
Decisión: 85 > 80, ir al hijo derecho

Paso 3: Cargar solo el nodo [85]
Memoria: [50|100|150] + [75|80] + [85] (24 bytes total)
Resultado: Encontrado
```

Este mismo índice de manera tradicional se tendría que cargar completamente desde el 10 hasta el 190. Como en forma de [[Array|array]].

## 2. Problema: Acceso Lento a Memoria Secundaria

**Solución con árboles:**
- Cada nodo se dimensiona para coincidir con el tamaño de página del disco
- Se minimiza el número de accesos a disco necesarios
- Principio de localidad: datos relacionados se almacenan juntos

## 3. Problema: Demasiados Desplazamientos En Búsqueda Binaria

**Comparación:**

```
Búsqueda binaria tradicional (1000 ítems): ~10 accesos a disco
Árbol B optimizado (1000 ítems): ~3 accesos a disco
```

## 4. Problema: Costo De Mantener Orden (Reorganizaciones Masivas)

**Solución con árboles:**
- **Reorganizaciones locales**: Solo se afectan los nodos en el camino de inserción/eliminación
- **Balanceo automático**: Mantiene eficiencia sin reorganización completa
- **Divisiones y fusiones**: Operaciones locales que no afectan todo el índice

# Clasificación De Árboles Para Índices

## Árboles Binarios

**Definición:** Cada nodo tiene máximo dos hijos (izquierdo y derecho).

**Estructura básica:**

```
      50
     /  \
   30    70
  /  \   /  \
20  40 60  80
```

**Características:**

- Cada nodo contiene una sola clave
- Hijo izquierdo < nodo padre < hijo derecho
- Altura puede ser O(log n) en el mejor caso, O(n) en el peor

**Ventajas:**

- Implementación simple
- Búsqueda, inserción y eliminación en O(log n) promedio

**Desventajas:**

- Pueden degenerarse en listas enlazadas (altura O(n))
- No optimizados para almacenamiento en disco
- Muchos accesos a disco por la altura

**Uso en bases de datos:** Raramente usados como índices principales por su altura excesiva.

## Árboles AVL

**Definición:** Árboles binarios auto-balanceados donde la diferencia de altura entre subárboles izquierdo y derecho nunca excede 1.

**Característica de balance:**

```
Factor de balance = altura(subárbol_derecho) - altura(subárbol_izquierdo)
Factor de balance ∈ {-1, 0, 1}
```

**Ejemplo de rotación AVL:**

```
Antes (desbalanceado):     Después (balanceado):
      10                        20
       \                       /  \
        20                    10   30
         \
          30
```

**Ventajas:**

- Garantiza altura O(log n)
- Búsquedas muy eficientes y predecibles
- Auto-balanceo automático

**Desventajas:**

- Rotaciones costosas en inserciones/eliminaciones
- Cada nodo solo tiene una clave (muchos nodos = muchos accesos a disco)
- No optimizado para sistemas de archivos

**Uso en bases de datos:** Usados en memoria RAM para índices pequeños, no para almacenamiento en disco.

## Árboles B

**Definición:** Árboles balanceados donde cada nodo puede contener múltiples claves y tener múltiples hijos. Diseñados específicamente para almacenamiento en disco.

**Estructura del nodo:**

```
Nodo B (orden m):
[K1|K2|K3|...|Kn] donde n ≤ m-1
[P0|P1|P2|...|Pn] donde Pi son punteros a hijos
```

**Ejemplo de Árbol B de orden 3:**

```
       [30|60]
      /   |   \
   [10|20] [40|50] [70|80|90]
```

**Propiedades:**

- Todos los nodos hoja están al mismo nivel
- Cada nodo (excepto raíz) tiene entre ⌈m/2⌉-1 y m-1 claves
- Cada nodo interno tiene entre ⌈m/2⌉ y m hijos
- Las claves en cada nodo están ordenadas

**Ventajas:**

- **Optimizado para disco**: Cada nodo = una página de disco
- **Altura mínima**: O(log_m n) donde m es el orden del árbol
- **Reorganizaciones locales**: Solo afectan el camino de la operación
- **Buen factor de ocupación**: ~50% mínimo

**Desventajas:**

- Más complejo de implementar que árboles binarios
- Puede desperdiciar espacio en nodos no llenos
- Búsquedas dentro del nodo requieren búsqueda secuencial o binaria

## Árboles B*

**Definición:** Variación de los árboles B que mantiene una ocupación mínima del 66% en lugar del 50%.

**Diferencia clave:**

- Antes de dividir un nodo lleno, intenta redistribuir claves con nodos hermanos
- Solo divide cuando tanto el nodo como su hermano están llenos

**Proceso de inserción mejorado:**

```
1. Si el nodo no está lleno → insertar directamente
2. Si el nodo está lleno pero hermano no → redistribuir
3. Si ambos están llenos → dividir en tres nodos (2/3 llenos cada uno)
```

**Ventajas sobre B:**

- **Mayor utilización de espacio**: 66% vs 50%
- **Menos divisiones**: Reduce reorganizaciones
- **Mejor rendimiento**: Menos nodos = menos accesos a disco

**Desventajas:**

- **Más complejo**: Lógica de redistribución adicional
- **Operaciones más costosas**: Verificar hermanos antes de dividir

## Árboles B+

**Definición:** Variación de los árboles B donde:

- Solo las hojas contienen datos reales
- Los nodos internos solo contienen claves de navegación
- Las hojas están enlazadas secuencialmente

**Estructura distintiva:**

```
Nodos internos (solo claves):     [30|60]
                                 /   |   \
Nodos hoja (datos+enlace):  [10,datos|20,datos]→[30,datos|50,datos]→[70,datos|80,datos]
```

**Características únicas:**

- **Separación de índice y datos**: Nodos internos vs. hojas
- **Enlace secuencial**: Hojas conectadas como lista enlazada
- **Duplicación de claves**: Las claves aparecen tanto en nodos internos como en hojas

**Ventajas:**

- **Recorrido secuencial eficiente**: Perfecto para rangos (BETWEEN)
- **Mejor factor de ocupación**: Nodos internos más pequeños
- **Operaciones de rango**: O(log n) + k, donde k es el número de resultados
- **Separación clara**: Índice separado de datos

**Desventajas:**

- **Duplicación de claves**: Ligero overhead de espacio
- **Complejidad adicional**: Mantener enlaces entre hojas

# Comparación Práctica

**Ejemplo con 1,000,000 de registros:**

|Tipo de Árbol|Altura Típica|Accesos a Disco|Ocupación|Uso Principal|
|---|---|---|---|---|
|Binario|~20|20|N/A|Memoria RAM|
|AVL|~20|20|N/A|Memoria RAM|
|B (ord. 100)|~3|3|50%|Índices en disco|
|B* (ord. 100)|~3|3|66%|Índices optimizados|
|B+ (ord. 100)|~3|3 + rango|66%|RDBMS modernos|

# Uso En Sistemas De Bases De Datos Reales

**Árboles B:** PostgreSQL, muchos sistemas de archivos **Árboles B+:** MySQL (InnoDB), SQL Server, Oracle, SQLite __Árboles B_:_* Menos comunes, algunos sistemas especializados

Los **árboles B+** dominan en RDBMS modernos porque combinan eficiencia en búsquedas puntuales con excelente rendimiento en consultas de rango, que son muy comunes en aplicaciones de bases de datos.
