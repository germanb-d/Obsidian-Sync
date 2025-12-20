---
Categoria: Sistemas
Materia: [[Base de Datos 1]]
tags:
---

![[BD1 Clase6 - Transacciones.pdf]]

# Definición

Colección de operaciones que forman una única unidad lógica de trabajo.

## Propiedades - ACID

Esto responde a la pregunta de porque es una única unidad lógica de trabajo.

- Atomicidad
- Consistencia
- Aislamiento
- Durabilidad

### A - Atomicidad / Atomicity

Definición: **Todas las operaciones de la transacción se ejecutan o NO se ejecuta ninguna**

Concepto "todo o nada":

- Si la transacción completa → todas las operaciones se aplican
- Si la transacción falla → ninguna operación se aplica
- No puede quedar a medias

Ejemplo:

```
Transferencia bancaria:
1. Restar 100 de cuenta A
2. Sumar 100 a cuenta B

Atomicidad garantiza:
✓ Ambas operaciones se ejecutan (transferencia exitosa)
✗ Ninguna se ejecuta (transferencia fallida)
✗ NUNCA: Solo se resta de A pero no se suma a B
```

Cómo se implementa:

Con **Bitácora (Log)**:

- Se registran todas las operaciones antes de hacerlas
- Si falla la transacción → **UNDO** (deshacer todo)
- Si completa → **COMMIT** (confirmar todo)

### C - Consistencia / **C**onsistency

Definición: **La ejecución aislada de la transacción conserva la consistencia de la BD**

Concepto:

- La BD comienza en un **estado consistente**
- La transacción se ejecuta
- La BD termina en un **estado consistente**
- Los **invariantes** (reglas de negocio) se mantienen

Ejemplo de invariante:

```
Regla: A + B = 100 (la suma total debe ser siempre 100)

Estado inicial: A=60, B=40 (60+40=100) ✓

Transacción:
A = A - 20 = 40
B = B + 20 = 60

Estado final: A=40, B=60 (40+60=100) ✓

La consistencia se mantiene
```

Cómo se implementa:

Responsabilidad compartida:

1. **El programador**: Debe escribir transacciones correctas que respeten las reglas
2. **El DBMS**: Verifica restricciones (claves primarias, foráneas, checks)

En entornos concurrentes:

- **Planificaciones serializables** garantizan consistencia
- Si una planificación NO es serializable → puede violar consistencia

Ejemplo de inconsistencia:

```
Invariante: A = 0 o B = 0 (al menos uno debe ser cero)
Inicial: A=0, B=0 ✓

Planificación NO serializable:
T0: READ(A)=0 → B=B+1=1
T1: READ(B)=0 → A=A+1=1

Estado final: A=1, B=1 ✗
Viola el invariante (ninguno es cero)
```

Relacionado con:

- **Seriabilidad**: Garantiza consistencia en entornos concurrentes
- **Restricciones de integridad**: Claves, checks, triggers
- **Retroceso en cascada**: Puede causar inconsistencia si no se maneja bien

### I - Aislamiento / Isolation

Definición: **Cada transacción ignora el resto de las transacciones que se ejecutan concurrentemente, actúa como si fuera única**

Concepto:

- Una transacción **no debe ver** los cambios intermedios de otras transacciones
- Cada transacción se ejecuta como si estuviera **sola** en el sistema
- Los resultados deben ser equivalentes a alguna ejecución en serie

Ejemplo del problema sin aislamiento:

```
T0: A=100 → A=50
T1: Lee A=50 (valor intermedio no confirmado)
T0: ABORT (deshace, A vuelve a 100)
T1: Usó un valor incorrecto (50) que nunca debió ver
```

Cómo se implementa:

Con **Bloqueos (Locks)**:

- **Lock compartido (Lock_c)**: Para lecturas
- **Lock exclusivo (Lock_e)**: Para escrituras
- **Protocolo de dos fases**: Garantiza seriabilidad (aislamiento completo)

> [!NOTE] Regla clave
> Una transacción NO puede leer/usar datos modificados por otra transacción que no haya hecho COMMIT

Ejemplo con bloqueos:

```
T0: Lock_e(A)
    WRITE(A)          // A modificado pero no confirmado
    
T1: Lock_c(A)         // Intenta leer A
    [ESPERA]          // Debe esperar (aislamiento)
    
T0: COMMIT            // Confirma cambios
    Unlock(A)
    
T1: READ(A)           // Ahora puede leer (valor confirmado)
```

Problema del retroceso en cascada:

```
Sin aislamiento adecuado:
T1 usa dato de T0 (no confirmada)
T0 aborta
T1 debe abortar también (retroceso en cascada)

Con aislamiento (bloqueos de dos fases):
T1 espera hasta que T0 haga COMMIT
No hay retroceso en cascada
```

Relacionado con:

- **Planificaciones serializables**: Implementan aislamiento
- **Control de concurrencia**: Bloqueos, timestamps
- **Protocolo de dos fases**: Garantiza aislamiento completo

En entornos monousuario:

- El aislamiento es **trivial** (no hay otras transacciones)

### D - Durabilidad / Durability

Definición: **Una transacción terminada con éxito realiza cambios permanentes en la BD, incluso si hay fallos en el sistema**

Concepto:

- Una vez que una transacción hace **COMMIT**, sus cambios son **permanentes**
- Sobreviven a caídas del sistema, cortes de luz, fallos de hardware
- No se pueden perder

Ejemplo:

```
T0: Transferencia bancaria
    A = A - 100
    B = B + 100
    COMMIT ✓

[CORTE DE LUZ - Sistema cae]

Al recuperarse:
Los cambios de T0 DEBEN estar en la BD
(durabilidad garantizada)
```

Cómo se implementa:

Con **Bitácora en almacenamiento estable**:

Regla crítica:

```
<T Commit> debe grabarse en DISCO (no volátil) 
ANTES de considerar la transacción completa
```

Proceso:

```
1. Transacción ejecuta operaciones
2. Se registran en bitácora (buffer)
3. Se graba <T Commit> en DISCO
4. Ahora la transacción está "Cometida"
5. Los datos pueden ir a disco antes, durante o después
```

Estados y durabilidad:

```
Parcialmente Cometida:
- Última instrucción ejecutada
- <T Commit> AÚN NO en disco
- NO hay durabilidad todavía

Cometida:
- <T Commit> grabado en disco
- HAY durabilidad
- Cambios son permanentes
```

Recuperación garantiza durabilidad:

Después de una caída:

```
<T1 Start>
<T1, A, 100, 200>
<T1 Commit>        ← Commit en disco
[FALLO]

Recuperación: REDO(T1)
- A = 200 (se rehace aunque no esté en disco)
- Durabilidad garantizada por la bitácora
```

Almacenamiento estable:

- **Discos espejo (RAID 1)**: Duplicación
- **RAID 5**: Con paridad
- **Backups**: Copias en medios separados
- Resiste fallos de dispositivos individuales

Ejemplo completo:

```
T0: UPDATE Cuenta SET saldo=500 WHERE id=123
    COMMIT

Secuencia:
1. Se modifica en buffer (volátil)
2. Se registra en bitácora (buffer)
3. Se graba <T0 Commit> en DISCO ← PUNTO CRÍTICO
4. T0 está "Cometida" (durabilidad garantizada)
5. El saldo puede ir a disco después (con OUTPUT)

Si hay fallo antes del paso 3:
- No hay durabilidad, T0 se deshace (UNDO)

Si hay fallo después del paso 3:
- Hay durabilidad, T0 se rehace (REDO)
```

Relacionado con:

- **Bitácora**: Mecanismo principal de durabilidad
- **REDO**: Rehace transacciones confirmadas
- **Checkpoints**: Optimizan recuperación pero mantienen durabilidad
- **Almacenamiento estable**: Resiste fallos físicos

Relación entre las propiedades ACID:

Cómo se complementan:

```
Atomicidad + Durabilidad:
- Si COMMIT → cambios permanentes (durabilidad)
- Si ABORT → ningún cambio persiste (atomicidad)

Consistencia + Aislamiento:
- Transacciones correctas (consistencia)
- Ejecutadas como si fueran solas (aislamiento)
- = Resultado consistente garantizado

Aislamiento + Atomicidad:
- No veo cambios intermedios (aislamiento)
- Solo veo transacciones completas o nada (atomicidad)
```

Resumen con todo lo visto:

|Propiedad|Implementación principal|Conceptos relacionados|
|---|---|---|
|Atomicidad|Bitácora + UNDO|Estados, Abort, Rollback|
|Consistencia|Seriabilidad + Restricciones|Invariantes, Planificaciones serializables, Grafos de precedencia|
|Aislamiento|Bloqueos + Dos fases|Control de concurrencia, Retroceso en cascada, Deadlocks|
|Durabilidad|Bitácora en disco + REDO|Commit en disco, Almacenamiento estable, Recuperación|

Ejemplo integrador:

Transferencia bancaria con ACID:

```
BEGIN TRANSACTION
  UPDATE Cuenta SET saldo = saldo - 100 WHERE id = 1
  UPDATE Cuenta SET saldo = saldo + 100 WHERE id = 2
COMMIT

ATOMICIDAD:
- Ambas operaciones o ninguna
- Si falla → UNDO ambas

CONSISTENCIA:
- Invariante: suma_total_saldos = constante
- Se mantiene antes y después

AISLAMIENTO:
- Lock_e en ambas cuentas
- Nadie ve valores intermedios
- Protocolo de dos fases

DURABILIDAD:
- <T Commit> grabado en disco
- Después de fallo → REDO
- Cambios permanentes garantizados
```

Conclusión:

ACID es el **contrato** que garantiza una BD transaccional:

- **A**: Todo o nada (no quedan a medias)
- **C**: Siempre correcta (respeta reglas)
- **I**: No interfieren entre sí (como si fueran solas)
- **D**: Una vez confirmada, permanente (sobrevive fallos)

Todo lo que vimos (bitácora, bloqueos, seriabilidad, recuperación, checkpoints) son los **mecanismos** que implementan estas propiedades.

## Estado De Una Transacción

![[BD1 Clase6 - Transacciones.pdf#page=4&rect=36,214,663,494|BD1 Clase6 - Transacciones, p.4]]

- **Activa**: estado inicial, estado normal durante la ejecución.
- **Parcialmente** Cometida: después de ejecutarse la última instrucción
- **Fallada**: luego de descubrir que no puede seguir la ejecución normal
- **Abortada**: después de haber retrocedido la transacción y restablecido la BD al estado anterior al comienzo de la transacción.
	- Reiniciar la Transacción: En caso de error de Hardware o Software
	- Cancelar la Transacción: En caso de error de logica
- **Cometida**: tras completarse con éxito.

## Uso De Transacciones

- **En sistemas monousuarios**: Más raro a menos que estemos practicando como nuestro caso, acá no puede haber dos personas accediendo al mismo dato.
- **En sistemas concurrentes**: Una BD en un solo servidor con mucha gente trabajando con esta a la vez.
- **En sistemas distribuidos**: Una sola BD lógica, pero está instalado en varios servidos conectados por una misma red. (no la vemos en esta materia).

# Ejemplo

## Explicación Base De Como Se Ejecuta

```mySQL
READ(A)
A := A - 100
WRITE(A)
READ(B)
B := B + 100
WRITE(B)
```

```
Instrucción 1-5 → [Estado: ACTIVA]
Instrucción 6 (última) → [Estado: PARCIALMENTE COMETIDA]
                         ↓
            Grabar <T Commit> en disco
                         ↓
                  [Estado: COMETIDA]
```

La diferencia es ese paso crítico de asegurar el commit en almacenamiento persistente, que es lo que garantiza que si el sistema falla justo después, podremos recuperar la transacción.

- **Parcialmente cometida** inmediatamente después de ejecutar la instrucción 6 (WRITE)
- **Cometida** después de grabar exitosamente `<T Commit>` en el disco (en la bitácora, significa que registre que se realizó la transacción en el disco, no necesariamente los datos de esta)

## Explicación De Interacciones De la Memoria

![[Transacción-1765574248651.webp|657x228]]

### 1. Memoria Local De la Transacción (t)

**Hardware:** Registros del CPU + RAM del proceso
- Son las variables que usa tu programa en ejecución
- Viven en la memoria RAM asignada al proceso de la transacción
- **Volátil:** Se pierde si el proceso termina o hay un fallo

### 2. Pool De Buffers (Memoria De la BD)

**Hardware:** RAM del servidor de [[Base de Datos]]
- Es un área de memoria RAM dedicada que el DBMS reserva para cachear datos
- Actúa como caché entre las transacciones y el disco
- **Volátil:** Se pierde si el servidor se cae o reinicia
- Similar conceptualmente a la caché L1/L2/L3, pero a nivel de software

### 3. Disk Blocks De la BD

**Hardware:** Almacenamiento no volátil
- **SSD/HDD:** El almacenamiento físico del servidor
- **Almacenamiento estable:** Puede incluir discos espejo (RAID), backups
- **Nube:** Podría ser almacenamiento distribuido (AWS RDS, Google Cloud [[SQL]])
- **No volátil:** Los datos persisten aunque se apague el servidor

## Explicación Paso a Paso

```
1. READ(A, a1)
2. a1 := a1 - 100
3. WRITE(A, a1)
4. READ(B, b1)
5. b1 := b1 + 100
6. WRITE(B, b1)
```

### Instrucción 1: READ(A, a1)

1. La transacción pregunta: "¿Está A en el pool de buffers?"
    - **SI está:** Copia el valor de A desde el pool → variable local `a1`
    - **NO está:**
        - Ejecuta `INPUT(A)`: trae el [[Bloque]] con A desde **disco → pool de buffers** (vía SO)
        - Luego copia el valor de A desde el pool → variable local `a1`

**Resultado:** `a1` tiene el valor de A (supongamos a1 = 1000)

---

### Instrucción 2: `A1 := A1 - 100`

- Operación aritmética **solo en memoria local** de la transacción
- No involucra pool de buffers ni disco

**Resultado:** `a1 = 900` (solo en memoria local)

---

### Instrucción 3: `WRITE(A, a1)`

- Copia el valor de `a1` (900) → actualiza A en el **pool de buffers**
- **NO se escribe al disco todavía** (eso depende de la política del DBMS)

**Resultado:** A = 900 en el pool de buffers

---

### Instrucción 4: `READ(B, b1)`

1. La transacción pregunta: "¿Está B en el pool de buffers?"
    - **SI está:** Copia el valor de B desde el pool → variable local `b1`
    - **NO está:**
        - Ejecuta `INPUT(B)`: trae el [[Bloque]] con B desde **disco → pool de buffers**
        - Luego copia el valor de B desde el pool → variable local `b1`

**Resultado:** `b1` tiene el valor de B (supongamos b1 = 2000)

---

### Instrucción 5: `B1 := B1 + 100`

- Operación aritmética **solo en memoria local**

**Resultado:** `b1 = 2100` (solo en memoria local)

---

### Instrucción 6: `WRITE(B, b1)`

- Copia el valor de `b1` (2100) → actualiza B en el **pool de buffers**
- **NO se escribe al disco todavía**

**Resultado:** B = 2100 en el pool de buffers

---

## `READ`/`WRITE` Y `INPUT`/`OUTPUT`

- **READ/WRITE:** Son operaciones de la transacción (nivel lógico)
- **INPUT/OUTPUT:** Son operaciones del sistema de gestión de buffers (nivel físico, controladas por el DBMS y SO)

La transacción **solo usa READ y WRITE**. El sistema decide cuándo hacer INPUT/OUTPUT según sus políticas.

# Estructura De Almacenamiento

## Almacenamiento Volátil

- Se pierde la información cuando hay un fallo del sistema o se corta la energía
- Ejemplo: **RAM**, **registros del CPU**

## Almacenamiento no Volátil

- La información **persiste** aunque se apague el sistema
- Se pierde solo ante fallos físicos del dispositivo
- Ejemplo: **SSD**, **HDD**

## Almacenamiento Estable

- Replica la información en **varios medios no volátiles independientes**
- Se actualiza de forma **controlada** para mantener consistencia
- Resiste fallos individuales de dispositivos
- Objetivo: asegurar que los datos se mantengan disponibles ante cualquier fallo

### Ejemplos De Almacenamiento Estable

Discos Espejo (Mirroring - RAID 1)

- Dos discos con la misma información **duplicada**
- Si uno falla, el otro mantiene todos los datos

RAID 5 (con 3 discos)

- Cada disco almacena:
    - Datos particulares propios
    - Información de **paridad** distribuida entre los 3 discos
- La paridad permite **reconstruir** los datos de cualquier disco que falle
- Si un disco se rompe:
    - Los otros dos pueden reconstruir la información faltante usando la paridad
    - Las consultas se vuelven **más lentas** pero la BD sigue operativa
    - Da tiempo para reemplazar el disco defectuoso sin perder datos

# Fallos

## Sin Perdida De Información

Si yo solo leo para imprimir en pantalla y falla, no hay consecuencias.

## Con Perdida De Información

### Fallo En la Transacción

**Lógicos**: interno a la transacción. No una falla de sintaxis, sino una falla de lógica como por ejemplo buscar por nombre y apellido en vez de por una clave, puede que funcione mucho tiempo, pero a la larga va a fallar.

**Del sistema**: bloqueos (deadlock) (bloqueos son la forma de manejar las concurrencias). Esto aborta la transacción fallida y retorna los datos correctos.

### Caída Del Sistema

Que se caiga el sistema. SO o DBMS 2

### Fallo De Disco

Es Necesario Tener Backups.

# Algoritmos De Tratamiento De Fallos

Objetivo dual:

- **Acciones preventivas**: llevadas a cabo durante el procesamiento normal de la transacción que permiten la recuperación ante fallos
- **Acciones correctivas**: llevadas a cabo después de ocurrir el fallo para restablecer el contenido de la BD a un estado que asegure ACID

## Detección De Fallos Inesperados

Cuando se realiza un **shutdown normal** (apagado controlado de la BD):

1. Se baja todo lo que está en memoria (buffers) a disco
2. Se guarda una **flag** indicando que la BD cerró correctamente

Al levantarse nuevamente, la BD revisa la flag:

- **Flag normal**: La BD cerró correctamente (mantenimiento programado) → No hay recuperación necesaria
- **Flag ausente o incorrecta**: La BD no cerró correctamente (fallo inesperado, corte de luz, crash) → Se activa el proceso de recuperación

# Recuperación En Caso De Fallo

Problema inicial:

- Re-ejecutar: no sirve (podríamos duplicar operaciones)
- No Re-ejecutar: no sirve (perdemos datos)
- Problema central: modificar la BD sin garantía de que la transacción se va a cometer
- Solución: **indicar las modificaciones antes de hacerlas efectivas** → permite recuperar

Métodos De Recuperación:

- Basado en Bitácora
- Doble Paginación (no se toma)

# Basado En Bitácora (log)

**[[Registro]] histórico**: secuencia de actividades realizadas sobre la BD

- Idealmente se almacena en otra memoria física separada de la BD

Contenido de la bitácora:

```
<T iniciada>                    (cuando inicia la transacción)
<T, E, Va, Vn>                  (para cada dato que modifica)
  - T: Identificador de la transacción
  - E: Identificador del elemento de datos
  - Va: Valor anterior
  - Vn: Valor nuevo
<T Commit> o <T Abort>          (nunca ambos a la vez)
```

La transacción se va **registrando** en la bitácora **durante toda su ejecución**

Antes de una caída: #Parcial

- **No se puede hacer nada** (no sabemos cuándo ocurrirá)
- Lo único garantizado: podemos **recuperar** el estado de la BD usando la bitácora
Excelente pregunta, te la hago más clara:

## ¿Por Qué Usar Bitácora Si Igual Estoy Escribiendo a Disco?

La respuesta está en la **eficiencia** y el **tipo de escritura**.

Diferencia clave entre escribir bitácora vs escribir datos:

> [!NOTE] Escritura de BITÁCORA (Log)
> - Es **secuencial** (siempre al final del [[Archivo]])
> - Es **pequeña** (solo registra qué cambió: `<T, dato, Va, Vn>`)
> - Es **rápida** (append al final)
> - Es en un **solo lugar** del disco

> [!NOTE] Escritura de DATOS
> - Es **aleatoria** (los datos están dispersos en el disco)
> - Es **grande** (páginas completas, bloques enteros)
> - Es **lenta** (buscar la ubicación + escribir)
> - Puede estar en **múltiples lugares** del disco

### Ejemplo Comparativo

Transacción que modifica 5 datos:

```
UPDATE Empleado SET saldo = 1000 WHERE id = 123
UPDATE Empleado SET saldo = 2000 WHERE id = 456
UPDATE Empleado SET saldo = 3000 WHERE id = 789
UPDATE Departamento SET presupuesto = 50000 WHERE id = 10
UPDATE Proyecto SET costo = 10000 WHERE id = 99
```

``` title:"Opción 1 - Escribir DATOS directamente a disco"
1. Buscar página de Empleado id=123 en disco → Escribir
2. Buscar página de Empleado id=456 en disco → Escribir
3. Buscar página de Empleado id=789 en disco → Escribir
4. Buscar página de Departamento id=10 en disco → Escribir
5. Buscar página de Proyecto id=99 en disco → Escribir

= 5 búsquedas aleatorias en disco
= 5 escrituras en diferentes ubicaciones
= MUY LENTO (ms por operación)
```

``` title:"Opción 2 - Escribir solo BITÁCORA"
Append al final del log:
<T1, Empleado.saldo[123], 800, 1000>
<T1, Empleado.saldo[456], 1500, 2000>
<T1, Empleado.saldo[789], 2500, 3000>
<T1, Departamento.presupuesto[10], 40000, 50000>
<T1, Proyecto.costo[99], 8000, 10000>
<T1 Commit>

= 1 escritura secuencial
= Todo junto al final del archivo
= MUY RÁPIDO (μs por operación)
```

Entonces, ¿cuándo se escriben los datos reales al disco?

El DBMS optimiza las escrituras:

```
Durante la transacción:
- Escrituras → solo bitácora (rápido)
- Datos → quedan en buffer (memoria)

Después del COMMIT:
- Bitácora → ya está en disco
- Datos → se escriben después, cuando convenga
```

## Dos Técnicas De Bitácora

### Modificación Diferida De la BD:

- Las operaciones **WRITE se aplazan** hasta que la transacción esté parcialmente cometida
- Solo cuando llega al commit se actualiza la bitácora y la BD
- Características:
    - O se graba toda la transacción con commit, o no se graba nada
    - **No necesita valor viejo** en la bitácora (Va no es necesario)
    - Hace la BD más lenta
    - Evita volver atrás en caso de fallos
    - Evita almacenar datos de transacciones incompletas

**Ejemplo de bitácora con modificación diferida**

```
<T0 Start>
<T0, A, 900>        (solo valor nuevo)
<T0, B, 2100>       (solo valor nuevo)
<T0 Commit>
```

**Recuperación ante un fallo**

**REDO (Ti)**: Para toda Ti que tenga `<Start>` y `<Commit>` en la bitácora

- Sobrescribe los datos en disco con los valores de la bitácora
- No sabemos si el disco se actualizó después del commit, entonces directamente **sobrescribimos** (más rápido que comparar)
- **Siempre se realiza** en modificación diferida (nunca graba sin commit)

Si no tiene Commit entonces se ignora, dado que no llegó a hacer algo en la BD.

### Modificación Inmediata De la BD:

- La actualización de la BD se realiza **mientras la transacción está activa**
- **PERMITE** (no lo hace siempre, solo está habilitada) que la BD pueda ir al disco cuando quiera (OUTPUT)
- El [[Registro]] paso a paso sigue en la bitácora, aunque no espera al commit
- **Necesita valor viejo y nuevo** (Va y Vn)

**Ejemplo de bitácora con modificación inmediata**

```
<T0 Start>
<T0, A, 1000, 900>    (valor anterior y nuevo)
<T0, B, 2000, 2100>   (valor anterior y nuevo)
<T0 Commit>
```

**Recuperación ante un fallo**

**REDO(Ti)**: Para toda Ti que tenga `<Start>` y `<Commit>` en la bitácora

- Sobrescribe los datos en disco con los valores de la bitácora
- No sabemos si el disco se actualizó después del commit, entonces directamente **sobrescribimos** (más rápido que comparar)
- **Siempre se realiza** en modificación diferida (nunca graba sin commit)

**UNDO(Ti)**: Para toda Ti que tenga `<Start>` y NO tenga `<Commit>` (tenga abort o no)

- Sobrescribe con los **datos viejos** (Va)
- Deja grabados los datos que tenía al iniciar la transacción
- **Solo necesario** en modificación inmediata

## Buffers De Bitácora

**Problema**
Grabar en disco cada [[Registro]] de bitácora consume mucho tiempo Solución: Usar buffers en memoria

> [!NOTE] Regla fundamental
> **"Siempre graba primero la Bitácora y luego la BD"**

**Momento crítico del commit**

- Una transacción está **parcialmente cometida** después de grabar `<T Commit>` en **memoria no volátil**
- Un `<T Commit>` en disco implica que **todos los registros anteriores** de esa transacción ya están en memoria no volátil

Después de una caída:

- **Solo se revisa la bitácora que está grabada en disco** #Parcial

# Puntos De Verificación (Checkpoints)

## Qué Es Un Checkpoint

- Marca que **todas las transacciones en volátil terminaron** y todo está OK en disco
- Se realiza una **pausa** para bajar todo a disco y hacer el checkpoint
- En caso de fallo, solo necesitamos recuperar transacciones que comenzaron **después del último checkpoint**

## Cuándo Se Coloca Un Checkpoint

- Cuando la **memoria está llena** y debe bajar a disco
- Cada **X tiempo** (segundos)
- Se determina según el **máximo tiempo de recuperación** tolerable en caso de caída #Parcial

## Ventajas

- Evita revisar toda la bitácora desde el inicio
- Solo se revisa desde el último checkpoint hacia adelante
