
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
    
- segunda iteración → registro de usuarios
    
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


Aquí tienes una serie de flashcards basadas en el contenido de tu nota [[Agilidad]] : #Mazo/POO2/Agilidad

**Modelos de Desarrollo de Software**

-   Modelos de desarrollo de software → Describen cómo organizar el proceso de creación de un sistema.
-   Modelos estructurados funcionan bien cuando | requisitos estables, mucho presupuesto, tiempo de desarrollo no crítico
-   Problema de modelos estructurados → Los requisitos cambian constantemente.

**Modelos de Desarrollo Tradicionales**

-   Modelos de desarrollo tradicionales | Proceso Unificado (UP), Modelo en V, Ciclo de Vida en Espiral
-   Los modelos tradicionales derivan de → Modelo en Cascada

**Modelo en Cascada**

-   Modelo en Cascada
    ?
    Uno de los primeros modelos de desarrollo de software, basado en una secuencia lineal de etapas donde cada fase debe completarse antes de la siguiente.
-   Etapas típicas del Modelo en Cascada | Análisis, Diseño, Codificación, Pruebas, Operación, Mantenimiento
-   Problema del Modelo en Cascada
    ?
    El usuario recién puede ver o usar el sistema casi al final del proceso, lo que hace muy costoso corregir cambios o malentendidos en los requisitos.

**Proceso Unificado (UP)**

-   Proceso Unificado (UP)
    ?
    Modelo de desarrollo más organizado que el cascada, pero estructurado, que divide el desarrollo en fases principales y se basa en casos de uso.
-   Fases principales del Proceso Unificado (UP) | Inicio, Elaboración, Construcción, Transición
-   Características del Proceso Unificado (UP) | Basado en casos de uso, tiene iteraciones pero es planificado, funciona mejor con requisitos estables.
-   Problema del Proceso Unificado (UP) → Dificultad para adaptarse si los requisitos cambian a mitad del desarrollo.

**Modelo en V**

-   Modelo en V
    ?
    Evolución del modelo cascada, representado con forma de "V", donde cada etapa de desarrollo en el lado izquierdo tiene una etapa de prueba asociada en el lado derecho.
-   Desarrollo (Modelo en V) | Requisitos, Diseño del sistema, Diseño detallado, Implementación
-   Prueba (Modelo en V) | Prueba de aceptación, Prueba del sistema, Prueba de integración, Prueba unitaria
-   Características del Modelo en V | Cada fase se diseña, implementa y prueba; desarrollo secuencial y rígido; poco análisis de riesgos.

**Ciclo de Vida en Espiral**

-   Ciclo de Vida en Espiral combina → Modelo cascada y desarrollo iterativo
-   Proponente del Ciclo de Vida en Espiral → Barry Boehm
-   Actividades en cada ciclo (espiral) | Planificación, Análisis de riesgos, Desarrollo, Evaluación
-   Beneficios del Ciclo de Vida en Espiral → Permite ver avances, identificar problemas temprano, reducir riesgos.

**Limitaciones de los Modelos Tradicionales**

-   Los modelos tradicionales presentan problemas cuando | Los requisitos cambian mucho, se necesita desarrollar rápido, el cliente quiere ver resultados tempranos.

**Metodologías Ágiles**

-   Objetivo de las Metodologías Ágiles | Reducir malentendidos, entregar software más rápido, adaptarse a cambios.
-   Características principales de las Metodologías Ágiles | Desarrollo incremental, iteraciones cortas, comunicación constante con el cliente, menos documentación.
-   Las metodologías ágiles entregan frecuentemente → Versiones funcionales del sistema. <!--SR:!2026-03-12,1,230-->

**Manifiesto Ágil**

-   Manifiesto Ágil: El equipo es lo más importante ↔ Las personas son el principal factor de éxito.
-   Manifiesto Ágil: Menor documentación exhaustiva ↔ Crear documentos solo cuando son necesarios, claros y breves.
-   Manifiesto Ágil: Colaboración con el cliente ↔ Trabajar junto al cliente, recibir feedback constante.
-   Manifiesto Ágil: Respuesta al cambio ↔ El plan puede adaptarse a los cambios del proyecto.

**Idea Clave**

-   Modelos tradicionales | rígidos, secuenciales, cambios costosos
-   Metodologías ágiles | flexibles, iterativas, adaptadas a cambios

