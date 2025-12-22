---
Categoria: 
Materia: 
tags:
---

![[BD1 Clase7 - Transacciones Entornos Concurrentes.pdf]]

# Definición

**Concurrente** significa que múltiples [[Transacciones]] se ejecutan simultáneamente y pueden acceder a los mismos datos.

Problema de la serialidad pura: Si dos transacciones quieren manejar el mismo dato y funcionan en **serie estricta** (primero se ejecuta completamente una, después la otra), el sistema se vuelve **inviable con el tiempo** por la lentitud que generaría.

## Ejemplo

![[Transacciones - Entornos Concurrentes-1765654170833.webp]]

T0 (Transferencia simple):

Resta 50 de 'a' y suma 50 a 'b' (transferencia de A hacia B)

T1 (Cálculo de interés):

Calcula el 10% de 'a', lo resta de 'a' y lo suma a 'b' (también una transferencia)

**Requisito de consistencia**: A + B debe mantenerse constante

*Planificaciones en serie*
1. **T0 → T1** (primero toda T0, después toda T1):
    
    - T0 ejecuta todas sus instrucciones
    - Luego T1 ejecuta todas sus instrucciones
    - Se respeta A+B ✓
2. **T1 → T0** (primero toda T1, después toda T0):
    
    - T1 ejecuta todas sus instrucciones
    - Luego T0 ejecuta todas sus instrucciones
    - Se respeta A+B ✓

Conclusión de la diapositiva: **"Ahora bien T0 T1 <> T1 T0"**

Esto significa que aunque **ambos órdenes son válidos**, producen **resultados finales diferentes** en los valores individuales de A y B, pero ambos mantienen la consistencia (A+B constante).

Planificación -> **Secuencia de ejecución de transacciones**

- Involucra todas las instrucciones de las transacciones
- Conserva el orden de ejecución dentro de cada transacción individual
- Un conjunto de $m$ transacciones genera $m!$ (factorial) planificaciones en serie posibles
	- Para 2 transacciones: 2! = 2 planificaciones en serie (T0→T1 y T1→T0)
- La **ejecución concurrente** NO necesita ser una planificación en serie (las instrucciones se pueden intercalar)
	- Pero debe ser **equivalente** a alguna planificación en serie para garantizar consistencia.

![[Transacciones - Entornos Concurrentes-1765654488852.webp]]

## Conclusiones

- El programa debe conservar la consistencia
- La inconsistencia temporal puede ser causa de inconsistencia en planificaciones en paralelo
- Una planificación concurrente debe equivaler a una planificación en serie
- Solo las instrucciones READ y WRITE son importantes y deben considerarse

---

# Conflictos

En planificaciones serializables solo se dan conflictos aquellas operaciones que modifican (`WRITE`).

> [!Ejemplo] Dos instrucciones **I1** (de T1) e **I2** (de T2) están en conflicto si:
> 1. Operan sobre el **mismo dato** (ej: ambas usan Q)
> 2. **Al menos una es un WRITE**
> 
> Casos de conflicto:
>
> - `READ(Q)` y `READ(Q)` → **NO HAY conflicto** (el orden no importa, ambas leen)
> - `READ(Q)` y `WRITE(Q)` → **SÍ HAY conflicto** (el READ leerá valores diferentes según el orden)
> - `WRITE(Q)` y `READ(Q)` → **SÍ HAY conflicto** (el READ leerá valores diferentes según el orden)
> - `WRITE(Q)` y `WRITE(Q)` → **SÍ HAY conflicto** (el estado final de Q será diferente según el orden)

---

## Planificaciones

Planificación (Schedule) -> Secuencia ordenada de instrucciones de varias transacciones, mostrando en qué orden se ejecutan.

Nosotros buscamos poder desarrollar una planificación con mayor intercalación de instrucciones (concurrencia) pero sin perder la fiabilidad que nos da la planificación en serie.

- **S** = una planificación (puede ser en serie o concurrente)
- **S'** = otra planificación de las mismas transacciones

``` title:Ejemplo
S (en serie):           S' (concurrente):
T0: READ(A)            T0: READ(A)
T0: WRITE(A)           T1: READ(B)
T1: READ(B)            T0: WRITE(A)
T1: WRITE(B)           T1: WRITE(B)
```

### Equivalencia En Conflictos

Dos planificaciones **S y S'** son **equivalentes en conflictos** si:

- Puedo transformar S en S' mediante **intercambios de instrucciones no conflictivas**
- Producen el mismo resultado final

Ejemplo de intercambio válido (NO conflicto):

```
T0: READ(A)    ↔    T1: READ(B)
```

Se pueden intercambiar porque operan sobre **datos distintos** (A y B)

Ejemplo de intercambio NO válido (SÍ conflicto):

```
T0: WRITE(A)   ✗   T1: READ(A)
```

NO se pueden intercambiar porque operan sobre el **mismo dato** y hay un **WRITE**

### Serializable En Conflictos

Definición formal: **S' es serializable en conflictos** si existe una planificación **S** tal que:

- S y S' son **equivalentes en conflictos**
- S es una **planificación en serie**

En otras palabras: Una planificación concurrente S' es **serializable** si puedo encontrar una planificación en serie S que produzca el mismo resultado.

``` title:Ejemplo
S (en serie):           S' (concurrente):
T0: READ(A)            T0: READ(A)
T0: WRITE(A)           T1: READ(B)
T1: READ(B)            T0: WRITE(A)
T1: WRITE(B)           T1: WRITE(B)
```

---

## Grafo De Precedencia

Para determinar si una planificación es serializable en conflictos

### Construcción Del Grafo

**Vértices**: Cada transacción = un vértice

**Aristas**: Se dibuja una arista **Ti → Tj** si ocurre alguno de estos casos:

1. Ti ejecuta **WRITE(Q)** antes que Tj ejecuta **READ(Q)**
2. Ti ejecuta **WRITE(Q)** antes que Tj ejecuta **WRITE(Q)**
3. Ti ejecuta **READ(Q)** antes que Tj ejecuta **WRITE(Q)**

La arista Ti → Tj significa: "Ti debe ejecutarse antes que Tj"

**Regla de verificación**:

- **SIN ciclos** → La planificación **ES serializable** en conflictos ✓
- **CON ciclos** → La planificación **NO ES serializable** en conflictos ✗

### Ejemplos

#### Ejemplo Sin Ciclo (ES serializable)

``` title:Planificación
T0: READ(A)
T0: WRITE(A)     ← T0 termina con A antes
T1: READ(A)      ← T1 lee DESPUÉS (lee el valor de T0)
T1: WRITE(A)
```

``` title:Grafo
┌────┐        ┌────┐
│ T0 │ ────→  │ T1 │
└────┘        └────┘
```

**Aristas**:
- T0 lee A → T1 escribe A: **T0 → T1**
- T0 escribe A → T1 escribe A: **T0 → T1**

**Sin ciclos** → ES serializable (equivalente a T0→T1 en serie)

#### Ejemplo Con Ciclo (NO ES serializable)

``` title:Planificación
T0: READ(A)
T1: READ(A)
T1: WRITE(A)
T0: WRITE(A)
```

``` title:Grafo
┌────┐  ────→  ┌────┐
│ T0 │         │ T1 │
└────┘  ←────  └────┘
```

**Aristas**:
- T0 lee A → T1 escribe A: **T0 → T1**
- T1 lee A → T0 escribe A: **T1 → T0**

**Hay ciclo** (las flechas forman un círculo) → NO ES serializable

### Importancia

Este método permite verificar rápidamente si una planificación concurrente es válida sin tener que probar todas las $m!$ planificaciones en serie posibles.

Si una planificación es serializable en conflictos, garantiza que mantiene la **consistencia** de la BD aunque las transacciones se ejecuten de forma **intercalada**.

---

# Control De Concurrencia

## Basado En Hora De Entrada

- **Jamás se usa en BD reales**
- Se ve solo porque está en el plan de la materia
- No es práctico en sistemas reales

## Bloqueos

- **Mecanismo más utilizado** para control de concurrencia
- Cada vez que una transacción usa un dato, lo bloquea

### Tipos De Bloqueos

#### Lock Compartido (Lock_c)

- **Uso**: Cuando solo quieres **leer** el dato (sin modificarlo)
- **Permite**: Que otras transacciones también puedan **leer** el mismo dato
- **Bloquea**: Que otras transacciones **escriban** el dato
- **Compatible**: Con otros Lock_c sobre el mismo dato

#### Lock Exclusivo (Lock_e)

- **Uso**: Cuando quieres **modificar** el dato (leer y escribir)
- **Bloquea**: Que otras transacciones **lean o escriban** el dato
- **Incompatible**: Con cualquier otro lock (ni Lock_c ni Lock_e)

#### Tabla De Compatibilidad

|Ya tiene|Solicita|¿Compatible?|
|---|---|---|
|Lock_c|Lock_c|✓ SÍ (ambas solo leen)|
|Lock_c|Lock_e|✗ NO (una lee, otra quiere escribir)|
|Lock_e|Lock_c|✗ NO (una escribe, otra quiere leer)|
|Lock_e|Lock_e|✗ NO (ambas quieren escribir)|

---

### Ciclo De Vida De Un Bloqueo

Una transacción debe:

1. **Obtener el dato**:
    - Si está **libre** → lo obtiene
    - Si tiene **Lock_c** y solicita **Lock_c** → lo obtiene (compatibles)
    - En otro caso → debe **esperar** (o abortar)
2. **Usar el dato**:
    - READ o WRITE según corresponda
3. **Liberarlo**:
    - Al hacer **commit** → libera todos sus locks
    - Al hacer **rollback/abort** → libera todos sus locks

``` title:"Ejemplo: Transaccion T0 (una transferencia)"
Lock_c(A)          // Pide permiso para leer A
READ(A)            // Lee el saldo de A
a := a - 100       // Calcula en memoria local
Lock_e(A)          // Ahora pide permiso exclusivo para escribir
WRITE(A)           // Escribe el nuevo valor
Lock_c(B)          // Pide permiso para leer B
READ(B)            // Lee el saldo de B
b := b + 100       // Calcula en memoria local
Lock_e(B)          // Pide permiso exclusivo para escribir
WRITE(B)           // Escribe el nuevo valor
COMMIT             // Libera todos los locks (A y B)
```

---

### Deadlock / Abrazo Mortal / Interbloqueo

Situación: Dos o más transacciones se **bloquean mutuamente** esperando recursos que la otra tiene.

``` title:Ejemplo
T0: Lock_e(A)           |  T1: Lock_e(B)
    ... opera con A     |    ... opera con B
    Lock_e(B) [ESPERA]  |     Lock_e(A) [ESPERA]
         ↓              |          ↓
    Necesita B          |     Necesita A
    pero T1 lo tiene    |     pero T0 lo tiene
```

```
T0                    T1
    │                     │
    ├─ Tiene: A           ├─ Tiene: B
    │                     │
    └─ Espera: B ──X──→   └─ Espera: A
              (bloqueado)
```

- T0 tiene bloqueado A y espera B
- T1 tiene bloqueado B y espera A
- **Ninguna puede continuar** → Deadlock

#### Prevención

##### Método 1: Tomar Todos Los Datos Necesarios Al Inicio

Funcionamiento:

```
Inicio de transacción:
1. Declarar TODOS los recursos que necesitará
2. Intentar obtener TODOS al mismo tiempo
3. Si tiene éxito → la transacción prosigue
4. Si NO tiene éxito → la transacción espera (o aborta)
5. Obtiene todos o ninguno
```

Ventajas:

- Elimina deadlocks completamente
- Simple de entender

Desventajas:

- **Posible inanición** (una transacción puede esperar eternamente)
- Requiere saber de antemano todos los recursos necesarios
- Bloquea recursos que quizás no use inmediatamente (ineficiente)

Mejora con prioridades:

- Asignar prioridades a las transacciones
- Las más antiguas tienen mayor prioridad
- Reduce (pero no elimina) la inanición

##### Método 2: Ordenar Los Recursos

Concepto:

```
Establecer un orden parcial de todos los datos
Los recursos se obtienen SIEMPRE en ese orden (o nada)
```

Ejemplo de orden:

```
Orden establecido: A < B < C < D

Correcto:
T0: Lock(A) → Lock(B) → Lock(D)  ✓
T1: Lock(A) → Lock(C)            ✓
T2: Lock(B) → Lock(D)            ✓

Incorrecto:
T3: Lock(C) → Lock(A)            ✗ (viola el orden)
```

Por qué previene deadlocks:

```
T0: Lock(A) ✓        T1: Lock(A) ⏳ (espera)
T0: Lock(B) ✓        
T0: usa A y B
T0: Unlock(A,B)
                     T1: Lock(A) ✓ (ahora sí)
                     T1: Lock(B) ✓
```

Si ambas siguen el orden, no pueden crear ciclos de espera.

Método 3: Uso de HDE (Hora De Entrada) con prioridades

Concepto:

- Las transacciones más antiguas (menor HDE) tienen **mayor prioridad**
- Cuando hay conflicto, la de menor prioridad aborta
- Evita inanición dando ventaja a las que llevan más tiempo

Ejemplo:

```
T0 (HDE = 100)  vs  T1 (HDE = 200)

Si ambas quieren los mismos recursos:
T0 tiene prioridad (HDE menor)
T1 aborta y se reinicia con nueva HDE
```

#### Detección

Algoritmo de detección:

Usar un **grafo de espera** (wait-for graph):

Construcción del grafo:

- **Vértices**: Cada transacción
- **Aristas**: Ti → Tj si Ti **espera** un recurso que tiene Tj

Regla de detección: **Si el grafo tiene ciclos → hay deadlock**

``` title:"Ejemplo sin deadlock"
T0 espera a T1
T1 espera a T2
T2 está libre

Grafo:
T0 → T1 → T2

Sin ciclos → No hay deadlock
```

``` title:"Ejemplo con deadlock"
T0 espera a T1
T1 espera a T2
T2 espera a T0

Grafo:
T0 → T1
 ↑    ↓
T2 ←─┘

Hay ciclo → HAY DEADLOCK
```

#### Recuperación

Una vez detectado el deadlock, hay que **romper el ciclo**:

**Selección de la víctima**: Elegir una transacción para abortar basándose en:
- Costo mínimo: La que haya hecho menos trabajo
- Menor cantidad de recursos bloqueados
- Menor tiempo de ejecución
- Menor cantidad de datos modificados

Criterios de selección:

```
Opciones:
1. La transacción más joven (mayor HDE)
2. La que tenga menos operaciones hechas
3. La que bloquee menos recursos
4. La que sea más fácil de reintentar
```

##### Hasta Donde Retroceder

Opciones:

1. **Abort completo**: Abortar toda la transacción y reiniciar desde el inicio
2. **Abort parcial**: Retroceder solo hasta el punto que causó el deadlock (más complejo)

Evitar inanición de la transacción retrocedida:

Problema:

```
T0 siempre es elegida como víctima
T0 aborta → reintenta → aborta → reintenta → ...
T0 nunca termina (inanición)
```

Soluciones:

- Llevar cuenta de cuántas veces fue abortada cada transacción
- Aumentar prioridad de transacciones abortadas múltiples veces
- Limitar el número de abortos (después de N abortos, se le da máxima prioridad)

Comparación de estrategias:

| Estrategia                      | Ventajas          | Desventajas                               |
| ------------------------------- | ----------------- | ----------------------------------------- |
| Prevención - Todos los recursos | Elimina deadlocks | Posible inanición, ineficiente            |
| Prevención - Orden de recursos  | Elimina deadlocks | Requiere orden predefinido                |
| Prevención - Prioridades HDE    | Evita inanición   | Muchos reintentos                         |
| Detección y recuperación        | Más flexible      | Overhead de detección, pérdida de trabajo |

Reducir casos de deadlock (buenas prácticas):

1. **Evitar que el usuario deba tomar decisiones durante bloqueos**
    
    - El usuario puede tardar mucho (minutos, horas)
    - Aumenta la probabilidad de deadlock
    - Automatizar decisiones cuando sea posible
2. **Mantener transacciones cortas**
    
    - Menos tiempo con recursos bloqueados
    - Menor ventana para deadlocks
3. **Acceder a recursos en orden consistente**
    
    - Todas las transacciones siguen el mismo orden
    - Reduce ciclos de espera
4. **Usar timeouts**
    
    - Si espera más de X segundos → abortar
    - Rompe deadlocks automáticamente (aunque no los detecte formalmente)

#### Ejemplo Práctico Completo

Deadlock:

```
T0: Lock_e(Cuenta_A)
T1: Lock_e(Cuenta_B)
T0: Lock_e(Cuenta_B) ⏳
T1: Lock_e(Cuenta_A) ⏳
→ DEADLOCK
```

Grafo de espera:

```
T0 → T1
 ↑    ↓
  └──┘
(ciclo detectado)
```

Recuperación:

```
1. Detectar el ciclo
2. Elegir víctima (por ejemplo T1, más joven)
3. Abortar T1:
   - Unlock(Cuenta_B)
   - UNDO(T1)
4. T0 puede continuar:
   - Lock_e(Cuenta_B) ✓
   - Completa su trabajo
   - Commit
5. T1 se reintenta después
```

Resumen:

Los deadlocks son un problema crítico en sistemas concurrentes que se puede:

- **Prevenir**: Con políticas estrictas de obtención de recursos
- **Detectar y recuperar**: Con grafos de espera y selección de víctimas
- **Reducir**: Con buenas prácticas de diseño de transacciones

La estrategia más común en BD reales es una **combinación**: timeouts + detección ocasional + transacciones bien diseñadas.

---

### Protocolo De Bloqueo De Dos Fases

**Problema a resolver**: Si hago `Lock_e`, `READ`, modifico y `WRITE`, estoy bloqueando el dato **todo el tiempo**, incluso cuando solo lo estoy procesando en memoria.

#### Solución - Dos Fases

Fase 1 - Crecimiento (obtener locks):

1. `Lock_c(dato)` → Pedir lock compartido
2. `READ(dato)` → Leer el valor
3. Procesar en **memoria local** (calcular, modificar variables locales)
4. Cuando termino de procesar, pedir `Lock_e(dato)` → Upgrade a exclusivo
5. `READ(dato)` nuevamente (por si cambió mientras procesaba)
6. `WRITE(dato)` → Escribir el resultado

Fase 2 - Decrecimiento (liberar locks): 7. `COMMIT` → Liberar todos los locks a la vez

#### Ventaja

- Mientras proceso en memoria, otros pueden seguir **leyendo** el dato (Lock_c es compatible)
- Solo bloqueo exclusivamente cuando voy a escribir (más eficiente)

Regla del protocolo de dos fases:

- **Fase crecimiento**: Solo se **piden** locks (compartidos o exclusivos, o en orden de c→e)
- **Fase decrecimiento**: Solo se **liberan** locks
- **No se puede pedir un lock después de haber liberado otro**

Garantía:

El protocolo de dos fases **garantiza seriabilidad en conflictos**, pero **NO evita deadlocks**.

``` title:Ejemplo
// FASE CRECIMIENTO
Lock_c(A)          // Pido lock compartido
READ(A)            
a := a - 100       // Proceso en memoria
Lock_e(A)          // Upgrade a exclusivo
WRITE(A)           
Lock_c(B)          // Pido otro lock compartido
READ(B)            
b := b + 100       // Proceso en memoria
Lock_e(B)          // Upgrade a exclusivo
WRITE(B)           
// FASE DECRECIMIENTO
COMMIT             // Libero TODOS los locks
```

---

### Granularidad De Los Bloqueos

Cuando hablamos de "bloquear datos", generalmente bloqueamos **tuplas** (filas):

Ejemplo - Transacción bancaria:

```
UPDATE Cuenta SET saldo = saldo - 100 WHERE id = 123
```

Se bloquea **toda la tupla** (fila) de la cuenta 123, no solo el campo `saldo`.

Problema: Si al mismo tiempo quiero actualizar otro campo de la misma cuenta:

```
UPDATE Cuenta SET tipo = 'Premium' WHERE id = 123
```

**No me lo permitirá** porque la tupla completa está bloqueada.

#### Niveles De Granularidad

De menor a mayor:

1. **Campo** (raro, muy fino)
2. **Tupla/Fila** (más común)
3. **Página** (bloque de tuplas)
4. **Tabla** (toda la tabla)
5. **Área/Tablespace** (conjunto de tablas)
6. **Base de Datos completa**

#### Casos De Bloqueos Más Amplios

Bloqueo de BD completa:

- Al **levantar de una caída** (durante recuperación)
- Durante un **backup completo**

Bloqueos más cortos pero importantes:

- **INSERT**: Bloquea la nueva fila hasta hacer commit
- **DELETE**: Puede tardar mucho por integridad referencial
- **Checkpoint**: Puede bloquear temporalmente para bajar todo a disco

```sql title:"Ejemplo - DELETE con integridad referencial"
DELETE FROM Departamento WHERE id = 4
```

El sistema debe verificar si hay empleados con `departamento_id = 4`:

Opciones según la configuración

1. **Borrado en cascada**: Borra todos los empleados del departamento 4 automáticamente
2. **Restrict**: Te impide borrar el departamento hasta que elimines los empleados manualmente
3. **Set NULL**: Los empleados quedan con `departamento_id = NULL`
4. **Preguntar**: El sistema pregunta al usuario qué hacer

Por esto algunos DELETE pueden **tardar mucho tiempo** (debe verificar y posiblemente borrar muchas filas relacionadas).

# Recuperación En Caso De Fallos

## Bitácora En Entornos Concurrentes

### Funcionamiento General

Idéntico a sistemas monousuarios

- La estructura y contenido de la bitácora es la misma
- `<T Start>`, `<T, dato, Va, Vn>`, `<T Commit>`, `<T Abort>`
- Se aplican las mismas reglas de REDO y UNDO

> [!Danger]
> La diferencia está en cómo se manejan los checkpoints

### Checkpoint En Sistemas Concurrentes

``` title:"Problema del checkpoint monousuario"
Colocarlo cuando ninguna transacción esté activa.
Puede que no exista el momento.
```

En un sistema concurrente con muchas transacciones simultáneas, **puede que nunca haya un momento** donde todas las transacciones hayan terminado.

---

``` title:"Solución - Checkpoint con lista"
Checkpoint<L>
L = lista de transacciones activas al momento del checkpoint
```

La lista L del checkpoint es como un "punto de referencia" que nos dice:

- **Antes del checkpoint**: Solo miramos lo que está en L
- **Después del checkpoint**: Miramos todo (estén o no en L)

Esto ahorra tiempo porque no revisamos [[Transacciones]] que ya sabemos que están completas y en disco.

#### Funcionamiento

1. El sistema hace checkpoint **en cualquier momento** (sin esperar)
2. Anota qué [[Transacciones]] están **activas** en ese instante
3. Guarda: `<Checkpoint, [T1, T3, T5]>` (ejemplo de lista L)

Ante un fallo - Proceso de recuperación: **UNDO y REDO según el caso**

Reglas generales:

- Transacción con `<Start>` y `<Commit>` → **REDO**
- Transacción con `<Start>` sin `<Commit>` → **UNDO**

> [!NOTE]
> Debemos buscar antes del Checkpoint solo aquellas [[Transacciones]] que estén en la lista

Esta es la regla clave:

1. **[[Transacciones]] que NO están en la lista L**:
    
    - Ya terminaron antes del checkpoint
    - Sus datos ya están confirmados en disco
    - **NO las revisamos** antes del checkpoint (optimización)
2. **[[Transacciones]] que SÍ están en la lista L**:
    
    - Estaban activas al momento del checkpoint
    - Pueden tener operaciones antes Y después del checkpoint
    - **SÍ las revisamos** antes del checkpoint
3. **[[Transacciones]] que comenzaron después del checkpoint**:
    
    - Todas se revisan (estén o no en la lista)
    - Se aplica REDO o UNDO según tengan commit

#### Ejemplo Completo De Recuperación

``` title:Bitacora
<T0 Start>
<T0, A, 100, 200>
<T0 Commit>                    ← Terminó ANTES del checkpoint
<T1 Start>
<T1, B, 300, 400>
<T2 Start>
<T2, C, 500, 600>
----------------------------------------
<Checkpoint, [T1, T2]>         ← Lista L = [T1, T2]
----------------------------------------
<T1, D, 700, 800>
<T1 Commit>                    ← T1 termina DESPUÉS
<T3 Start>                     ← T3 comienza DESPUÉS
<T3, E, 900, 1000>
<T2, F, 1100, 1200>
[FALLO DEL SISTEMA]            ← Caída aquí
```

##### Análisis Paso a Paso

> [!NOTE] Zona ANTES del checkpoint
> - **T0**: Ya terminó, NO está en lista L → **NO la revisamos** (ignorada)
> - **T1**: Está en lista L → **SÍ la revisamos** (operación B)
> - **T2**: Está en lista L → **SÍ la revisamos** (operación C)

> [!NOTE] Zona DESPUÉS del checkpoint
> - **T1**: Continuó → SÍ la revisamos (operación D)
> - **T2**: Continuó → SÍ la revisamos (operación F)
> - **T3**: Comenzó después → SÍ la revisamos (operación E)

##### Clasificación Para Recuperación

**T0**:
- NO está en lista → **Ignorada** (ya está en disco)
**T1**:
- En lista L
- Tiene `<T1 Commit>` → **REDO(T1)**
- Rehacer: B=400, D=800
**T2**:
- En lista L
- NO tiene commit → **UNDO(T2)**
- Deshacer: C vuelve a 500, F vuelve a 1100
**T3**:
- Comenzó después del checkpoint
- NO tiene commit → **UNDO(T3)**
- Deshacer: E vuelve a 900

##### Resumen Visual Del Proceso

```
ANTES del checkpoint:
├─ T0 (no en lista) → IGNORAR ✗
├─ T1 (en lista)    → REVISAR ✓
└─ T2 (en lista)    → REVISAR ✓

DESPUÉS del checkpoint:
├─ T1 (continúa)    → REVISAR ✓
├─ T2 (continúa)    → REVISAR ✓
└─ T3 (nueva)       → REVISAR ✓
```

#### Ventajas De Este Método

1. **No detiene el sistema** al hacer checkpoint
2. **Optimiza la recuperación**: No revisa [[Transacciones]] antiguas ya confirmadas
3. **Reduce tiempo de recuperación**: Solo procesa lo necesario
4. **Permite alta concurrencia**: El sistema sigue funcionando normalmente
