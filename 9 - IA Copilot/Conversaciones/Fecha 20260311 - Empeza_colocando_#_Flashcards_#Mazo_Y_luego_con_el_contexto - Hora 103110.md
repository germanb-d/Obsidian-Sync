---
epoch: 1773235870656
modelKey: "gemini-2.5-flash|google"
topic: "Generación de Flashcards y Formatos"



tags:
  - Conversaciones
---

**user**: Empeza colocando:
# Flashcards
#Mazo
Y luego con el contexto de {[[Nota Name]]} crea flashcards, estas pueden ser:
Single-Line Basic: Pregunta → respuesta
Single-Line Bidirectional: Info 1 ↔ Info 2 (Para estas tarjetas solo usa el simbolo ↔)
Multi-line Basic: 
Una pregunta general
? 
La respuesta
Multi-line Bidirectional:
Info 1
??
Info 2
[Context: Notes: 4 - Notas Rapidas/Agilidad.md]
[Timestamp: 2026/03/11 10:31:10]

**ai**: # Flashcards
#Mazo

## Contexto

Modelos de desarrollo de software → Describen cómo organizar el proceso de creación de un sistema
Modelos muy estructurados → Cada etapa debe completarse antes de pasar a la siguiente

Modelos estructurados funcionan bien cuando:
?
- Los requisitos del sistema son estables
- El proyecto tiene mucho presupuesto
- El tiempo de desarrollo no es crítico

Problema de modelos estructurados → Los requisitos cambian constantemente

## Modelos de desarrollo tradicionales

Modelos de desarrollo tradicionales conocidos:
?
- Proceso Unificado (UP)
- Modelo en V
- Ciclo de Vida en Espiral

Modelos tradicionales derivan de → Modelo en cascada

## Modelo en Cascada

Modelo en cascada → Uno de los primeros modelos de desarrollo de software
Modelo en cascada se basa en → Una secuencia lineal de etapas

Etapas típicas del Modelo en Cascada:
?
1. Análisis
2. Diseño
3. Codificación
4. Pruebas
5. Operación
6. Mantenimiento

Funcionamiento del Modelo en Cascada:
?
- Primero se analizan todos los requisitos.
- Luego se diseña el sistema.
- Después se programa.
- Finalmente se prueba y se entrega.

Problema del Modelo en Cascada:
?
El usuario recién puede ver o usar el sistema casi al final del proceso.
Esto genera problemas porque si los requisitos cambian o algo se entendió mal, puede ser muy costoso corregirlo.

## Proceso Unificado (UP)

Proceso Unificado (UP) → Modelo de desarrollo más organizado que el cascada, pero estructurado
Proceso Unificado (UP) se construye en partes (iteraciones) ↔ El modelo en cascada es lineal

Fases principales del Proceso Unificado:
?
1. Inicio (Inception)
2. Elaboración
3. Construcción
4. Transición

Características del Proceso Unificado:
?
- Se basa en casos de uso definidos por el usuario.
- Tiene iteraciones, pero el proceso sigue siendo bastante planificado.
- Funciona mejor cuando los requisitos no cambian demasiado.

Problema del Proceso Unificado → Si los requisitos cambian a mitad del desarrollo, puede ser difícil adaptarse.

## Modelo en V

Modelo en V → Evolución del modelo cascada
Modelo en V se llama así porque → El proceso se representa con forma de V

Lado izquierdo del Modelo en V → Etapas de desarrollo
Lado derecho del Modelo en V → Etapas de prueba

Etapas de desarrollo y prueba asociadas en el Modelo en V:
?
|Desarrollo|Prueba|
|---|---|
|Requisitos|Prueba de aceptación|
|Diseño del sistema|Prueba del sistema|
|Diseño detallado|Prueba de integración|
|Implementación|Prueba unitaria|

Características del Modelo en V:
?
- Cada fase se diseña, implementa y prueba antes de pasar a la siguiente.
- No tiene tanto análisis de riesgos como otros modelos.
- El desarrollo sigue siendo secuencial y bastante rígido.

## Ciclo de Vida en Espiral

Modelo espiral combina → Modelo cascada y desarrollo iterativo
Modelo espiral fue propuesto por → Barry Boehm

El proyecto en el modelo espiral se desarrolla en → Ciclos llamados espirales

Actividades en cada ciclo del Modelo en Espiral:
?
1. Planificación
2. Análisis de riesgos
3. Desarrollo
4. Evaluación

El Modelo en Espiral permite:
?
- Ver avances del proyecto
- Identificar problemas temprano
- Reducir riesgos

## Limitaciones de los modelos tradicionales

Modelos tradicionales fueron útiles porque:
?
- Solo grandes empresas desarrollaban software
- Los proyectos tenían presupuestos muy altos
- Los requisitos cambiaban poco

Problemas de los modelos tradicionales cuando:
?
- Los requisitos cambian mucho
- Se necesita desarrollar rápido
- El cliente quiere ver resultados tempranos

Para resolver los problemas de los modelos tradicionales aparecen → Las metodologías ágiles

## Metodologías Ágiles

Metodologías ágiles buscan → Hacer el desarrollo más flexible

Objetivo de las metodologías ágiles:
?
- Reducir malentendidos
- Entregar software más rápido
- Adaptarse a cambios

Características principales de las metodologías ágiles:
?
- Desarrollo incremental
- Iteraciones cortas
- Comunicación constante con el cliente
- Menos documentación

En metodologías ágiles se entregan versiones funcionales del sistema → De manera frecuente

Esto permite en metodologías ágiles:
?
- Detectar errores antes
- Ajustar requisitos
- Mejorar el producto continuamente

## Manifiesto Ágil

Manifiesto Ágil establece → Valores fundamentales para el desarrollo de software

### 1. El equipo es lo más importante

El equipo es el principal factor de éxito ↔ Un buen equipo es más importante que un entorno perfecto
Primero se forma el equipo y luego se organiza el trabajo ↔ El equipo es lo más importante

### 2. Menor documentación exhaustiva

Menor documentación exhaustiva no significa → Eliminar la documentación
La idea es crear documentos → Solo cuando son necesarios, que sean claros y breves, y apoyar la comunicación con el cliente

### 3. Colaboración con el cliente

Se prioriza trabajar junto al cliente y recibir feedback constante ↔ En lugar de depender exclusivamente de contratos rígidos

### 4. Respuesta al cambio

En metodologías tradicionales el plan debe seguirse estrictamente ↔ En metodologías ágiles el plan puede adaptarse a los cambios del proyecto
Esto permite reaccionar mejor cuando → Cambian los requisitos o aparecen nuevas necesidades

## Idea clave para recordar (muy importante)

Modelos tradicionales:
??
- Rígidos
- Secuenciales
- Cambios costosos

Metodologías ágiles:
??
- Flexibles
- Iterativas
- Adaptadas a cambios
[Timestamp: 2026/03/11 10:31:18]