
## Contexto

En el desarrollo de software existen diferentes **modelos de desarrollo** que describen **cómo organizar el proceso de creación de un sistema**.

Durante muchos años se utilizaron **modelos muy estructurados**, donde cada etapa debía completarse antes de pasar a la siguiente.

Estos modelos funcionan bien cuando:

- los **requisitos del sistema son estables**
    
- el **proyecto tiene mucho presupuesto**
    
- el **tiempo de desarrollo no es crítico**
    

Sin embargo, con el tiempo se observó que **los requisitos cambian constantemente**, por lo que estos modelos comenzaron a presentar problemas.

---

# Modelos de desarrollo tradicionales

Algunos modelos de desarrollo conocidos son:

- **Proceso Unificado (UP)**
    
- **Modelo en V**
    
- **Ciclo de Vida en Espiral**
    

Estos modelos **derivan del modelo en cascada**.

---

## Modelo en Cascada

El **modelo en cascada** es uno de los primeros modelos de desarrollo de software.

Se basa en una **secuencia lineal de etapas**, donde cada fase debe completarse antes de comenzar la siguiente.

Las etapas típicas son:

1. **Análisis**
    
2. **Diseño**
    
3. **Codificación**
    
4. **Pruebas**
    
5. **Operación**
    
6. **Mantenimiento**
    

Funcionamiento:

- Primero se analizan todos los requisitos.
    
- Luego se diseña el sistema.
    
- Después se programa.
    
- Finalmente se prueba y se entrega.
    

### Problema del modelo

El usuario **recién puede ver o usar el sistema casi al final del proceso**.

Esto genera problemas porque:

- si los requisitos cambian
    
- o si algo se entendió mal
    

puede ser **muy costoso corregirlo**.

En proyectos grandes esto implicaba **mucho tiempo de espera**.

---

## Proceso Unificado (UP)

El **Proceso Unificado** es un modelo de desarrollo más organizado que el cascada, pero sigue siendo bastante estructurado.
%%> Se diferencia con el de cascada en que este se contruye en partes (iteraciones) y el cliente puede ver avances %%
Divide el desarrollo en **fases principales**:

1. **Inicio (Inception)**
    
2. **Elaboración**
    
3. **Construcción**
    
4. **Transición**

Características:

- Se basa en **casos de uso definidos por el usuario**.
    
- Tiene **iteraciones**, pero el proceso sigue siendo bastante planificado.
    
- Funciona mejor cuando **los requisitos no cambian demasiado**.

> [!example] Ejemplo
> Sistema para una clínica.
> 1. **Inicio**  
>     Se define qué hará el sistema (pacientes, turnos, médicos).
> 2. **Elaboración**  
>     Se diseña la arquitectura del sistema.
> 3. **Construcción**  
>     Se programan los módulos.
> 4. **Transición**  
>     Se entrega el sistema al cliente.


Problema:

Si los **requisitos cambian a mitad del desarrollo**, puede ser difícil adaptarse.

---

## Modelo en V

El **modelo en V** es una evolución del modelo cascada.

Se llama así porque el proceso se representa con forma de **V**.

En el lado izquierdo se encuentran las **etapas de desarrollo**, y en el lado derecho las **etapas de prueba**.

Cada etapa de desarrollo tiene una etapa de prueba asociada.

|Desarrollo|Prueba|
|---|---|
|Requisitos|Prueba de aceptación|
|Diseño del sistema|Prueba del sistema|
|Diseño detallado|Prueba de integración|
|Implementación|Prueba unitaria|

Características:

- Cada fase se **diseña, implementa y prueba** antes de pasar a la siguiente.
    
- No tiene tanto **análisis de riesgos** como otros modelos.
    
- El desarrollo sigue siendo **secuencial y bastante rígido**.
    

Ejemplo:

Sistema de ventas online.

- Se definen los requisitos.
    
- Se diseña el sistema.
    
- Se programa.
    
- Luego se realizan pruebas en diferentes niveles.
    

---

## Ciclo de Vida en Espiral

El **modelo espiral** combina:

- el **modelo cascada**
    
- el **desarrollo iterativo**
    

Fue propuesto por **Barry Boehm**.

El proyecto se desarrolla en **ciclos llamados espirales**.

En cada ciclo se realizan cuatro actividades:

1. **Planificación**
    
2. **Análisis de riesgos**
    
3. **Desarrollo**
    
4. **Evaluación**
    

Esto permite:

- ver avances del proyecto
    
- identificar problemas temprano
    
- reducir riesgos
    

Ejemplo:

Sistema de banca online.

Primera espiral:

- se planifica el sistema de login
    
- se analizan riesgos de seguridad
    
- se desarrolla el módulo
    
- se evalúa
    

Segunda espiral:

- se planifican transferencias
    
- se analizan riesgos
    
- se desarrolla
    
- se evalúa
    

Esto proporciona **mejor visibilidad del proyecto**.

---

## Limitaciones de los modelos tradicionales

Estos modelos fueron muy útiles en el pasado porque:

- solo **grandes empresas desarrollaban software**
    
- los proyectos tenían **presupuestos muy altos**
    
- los **requisitos cambiaban poco**
    

Pero presentan problemas cuando:

- los requisitos cambian mucho
    
- se necesita desarrollar rápido
    
- el cliente quiere ver resultados tempranos
    

Para resolver estos problemas aparecen **las metodologías ágiles**.

---

# Metodologías Ágiles

Las metodologías ágiles buscan **hacer el desarrollo más flexible**.

Su objetivo es:

- reducir malentendidos
    
- entregar software más rápido
    
- adaptarse a cambios
    

Características principales:

- **desarrollo incremental**
    
- **iteraciones cortas**
    
- **comunicación constante con el cliente**
    
- **menos documentación**
    

En lugar de esperar hasta el final del proyecto, se **entregan versiones funcionales del sistema de manera frecuente**.

Esto permite:

- detectar errores antes
    
- ajustar requisitos
    
- mejorar el producto continuamente.
    

Ejemplo:

Si se desarrolla una aplicación web:

- primera iteración → login <!--SR:!2026-03-12,1,230-->
    
- segunda iteración → registro de usuarios <!--SR:!2026-03-12,1,226-->
    
- tercera iteración → sistema de pagos <!--SR:!2026-03-12,1,230-->
    

Cada iteración produce **una versión funcional del sistema**.

---

# Manifiesto Ágil

El **Manifiesto Ágil** establece valores fundamentales para el desarrollo de software.

## 1. El equipo es lo más importante

- Las personas son el principal factor de éxito.
    
- Un buen equipo es más importante que un entorno perfecto.
    
- Primero se forma el equipo y luego se organiza el trabajo.
    

---

## 2. Menor documentación exhaustiva

No significa eliminar la documentación, sino **evitar documentación innecesaria**.

La idea es:

- crear documentos **solo cuando son necesarios**
    
- que sean **claros y breves**
    
- apoyar la comunicación con el cliente.
    

---

## 3. Colaboración con el cliente

Se prioriza:

- trabajar junto al cliente
    
- recibir feedback constante
    

en lugar de depender exclusivamente de **contratos rígidos**.

---

## 4. Respuesta al cambio

En metodologías tradicionales:

- el plan debe seguirse estrictamente.
    

En metodologías ágiles:

- el plan puede **adaptarse a los cambios del proyecto**.
    

Esto permite reaccionar mejor cuando:

- cambian los requisitos
    
- aparecen nuevas necesidades.
    

---

# Idea clave para recordar (muy importante)

Modelos tradicionales:

- **rígidos**
    
- **secuenciales**
    
- cambios costosos.
    

Metodologías ágiles:

- **flexibles**
    
- **iterativas**
    
- adaptadas a cambios.
    

---

Si querés, también puedo hacerte **una versión ultra resumida tipo machete de parcial (1 hoja)** con:

- Cascada
    
- V
    
- Espiral
    
- Ágil
    

porque **esas comparaciones suelen aparecer muchísimo en exámenes de Ingeniería de Software**.
# Flashcards
#Mazo/POO2/Agilidad

## Contexto

Modelos de desarrollo de software → Describen cómo organizar el proceso de creación de un sistema <!--SR:!2026-03-12,1,226-->
Modelos muy estructurados → Cada etapa debe completarse antes de pasar a la siguiente <!--SR:!2026-03-12,1,226-->

Modelos estructurados funcionan bien cuando:
?
- Los requisitos del sistema son estables
- El proyecto tiene mucho presupuesto
- El tiempo de desarrollo no es crítico <!--SR:!2026-03-12,1,226-->

Problema de modelos estructurados → Los requisitos cambian constantemente <!--SR:!2026-03-12,1,226-->

## Modelos de desarrollo tradicionales

Modelos de desarrollo tradicionales conocidos:
?
- Proceso Unificado (UP)
- Modelo en V
- Ciclo de Vida en Espiral <!--SR:!2026-03-12,1,226-->

Modelos tradicionales derivan de → Modelo en cascada <!--SR:!2026-03-12,1,226-->

## Modelo en Cascada

Modelo en cascada → Uno de los primeros modelos de desarrollo de software <!--SR:!2026-03-12,1,226-->
Modelo en cascada se basa en → Una secuencia lineal de etapas <!--SR:!2026-03-12,1,226-->

Etapas típicas del Modelo en Cascada:
?
1. Análisis
2. Diseño
3. Codificación
4. Pruebas
5. Operación
6. Mantenimiento <!--SR:!2026-03-12,1,226-->

Funcionamiento del Modelo en Cascada:
?
- Primero se analizan todos los requisitos.
- Luego se diseña el sistema.
- Después se programa.
- Finalmente se prueba y se entrega. <!--SR:!2026-03-12,1,226-->

Problema del Modelo en Cascada:
?
El usuario recién puede ver o usar el sistema casi al final del proceso.
Esto genera problemas porque si los requisitos cambian o algo se entendió mal, puede ser muy costoso corregirlo. <!--SR:!2026-03-12,1,226-->

## Proceso Unificado (UP)

Proceso Unificado (UP) → Modelo de desarrollo más organizado que el cascada, pero estructurado <!--SR:!2026-03-12,1,226-->
Proceso Unificado (UP) se construye en partes (iteraciones) ↔ El modelo en cascada es lineal <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->

Fases principales del Proceso Unificado:
?
1. Inicio (Inception)
2. Elaboración
3. Construcción
4. Transición <!--SR:!2026-03-12,1,226-->

Características del Proceso Unificado:
?
- Se basa en casos de uso definidos por el usuario.
- Tiene iteraciones, pero el proceso sigue siendo bastante planificado.
- Funciona mejor cuando los requisitos no cambian demasiado. <!--SR:!2026-03-12,1,226-->

Problema del Proceso Unificado → Si los requisitos cambian a mitad del desarrollo, puede ser difícil adaptarse. <!--SR:!2026-03-12,1,226-->

## Modelo en V

Modelo en V → Evolución del modelo cascada <!--SR:!2026-03-12,1,226-->
Modelo en V se llama así porque → El proceso se representa con forma de V <!--SR:!2026-03-12,1,226-->

Lado izquierdo del Modelo en V → Etapas de desarrollo <!--SR:!2026-03-12,1,226-->
Lado derecho del Modelo en V → Etapas de prueba <!--SR:!2026-03-12,1,226-->

Etapas de desarrollo y prueba asociadas en el Modelo en V:
?
|Desarrollo|Prueba|
|---|---|
|Requisitos|Prueba de aceptación|
|Diseño del sistema|Prueba del sistema|
|Diseño detallado|Prueba de integración|
|Implementación|Prueba unitaria| <!--SR:!2026-03-12,1,226-->

Características del Modelo en V:
?
- Cada fase se diseña, implementa y prueba antes de pasar a la siguiente.
- No tiene tanto análisis de riesgos como otros modelos.
- El desarrollo sigue siendo secuencial y bastante rígido. <!--SR:!2026-03-12,1,226-->

## Ciclo de Vida en Espiral

Modelo espiral combina → Modelo cascada y desarrollo iterativo <!--SR:!2026-03-12,1,226-->
Modelo espiral fue propuesto por → Barry Boehm <!--SR:!2026-03-12,1,226-->

El proyecto en el modelo espiral se desarrolla en → Ciclos llamados espirales <!--SR:!2026-03-12,1,226-->

Actividades en cada ciclo del Modelo en Espiral:
?
1. Planificación
2. Análisis de riesgos
3. Desarrollo
4. Evaluación <!--SR:!2026-03-12,1,226-->

El Modelo en Espiral permite:
?
- Ver avances del proyecto
- Identificar problemas temprano
- Reducir riesgos <!--SR:!2026-03-12,1,226-->

## Limitaciones de los modelos tradicionales

Modelos tradicionales fueron útiles porque:
?
- Solo grandes empresas desarrollaban software
- Los proyectos tenían presupuestos muy altos
- Los requisitos cambiaban poco <!--SR:!2026-03-12,1,226-->

Problemas de los modelos tradicionales cuando:
?
- Los requisitos cambian mucho
- Se necesita desarrollar rápido
- El cliente quiere ver resultados tempranos

Para resolver los problemas de los modelos tradicionales aparecen → Las metodologías ágiles <!--SR:!2026-03-12,1,226-->

## Metodologías Ágiles

Metodologías ágiles buscan → Hacer el desarrollo más flexible <!--SR:!2026-03-12,1,226-->

Objetivo de las metodologías ágiles:
?
- Reducir malentendidos
- Entregar software más rápido
- Adaptarse a cambios <!--SR:!2026-03-12,1,226-->

Características principales de las metodologías ágiles:
?
- Desarrollo incremental
- Iteraciones cortas
- Comunicación constante con el cliente
- Menos documentación <!--SR:!2026-03-12,1,226-->

En metodologías ágiles se entregan versiones funcionales del sistema → De manera frecuente <!--SR:!2026-03-12,1,226-->

Esto permite en metodologías ágiles:
?
- Detectar errores antes
- Ajustar requisitos
- Mejorar el producto continuamente <!--SR:!2026-03-12,1,226-->

## Manifiesto Ágil

Manifiesto Ágil establece → Valores fundamentales para el desarrollo de software <!--SR:!2026-03-12,1,226-->

### 1. El equipo es lo más importante

El equipo es el principal factor de éxito ↔ Un buen equipo es más importante que un entorno perfecto <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->
Primero se forma el equipo y luego se organiza el trabajo ↔ El equipo es lo más importante <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->

### 2. Menor documentación exhaustiva

Menor documentación exhaustiva no significa → Eliminar la documentación <!--SR:!2026-03-12,1,226-->
La idea es crear documentos → Solo cuando son necesarios, que sean claros y breves, y apoyar la comunicación con el cliente <!--SR:!2026-03-12,1,226-->

### 3. Colaboración con el cliente

Se prioriza trabajar junto al cliente y recibir feedback constante ↔ En lugar de depender exclusivamente de contratos rígidos <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->

### 4. Respuesta al cambio

En metodologías tradicionales el plan debe seguirse estrictamente ↔ En metodologías ágiles el plan puede adaptarse a los cambios del proyecto <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->
Esto permite reaccionar mejor cuando → Cambian los requisitos o aparecen nuevas necesidades <!--SR:!2026-03-12,1,226-->

## Idea clave para recordar (muy importante)

Modelos tradicionales:
??
- Rígidos
- Secuenciales
- Cambios costosos <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->

Metodologías ágiles:
??
- Flexibles
- Iterativas
- Adaptadas a cambios <!--SR:!2026-03-12,1,226!2026-03-12,1,226-->