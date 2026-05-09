---
epoch: 1773235870656
modelKey: "gemini-2.5-flash|google"
topic: "Generación de Flashcards y Formatos"



tags:
  - Conversaciones
---

**user**: Empeza colocando:
# Flashcards
^learnkit-904818607
Q | #Mazo Y luego con el contexto de {[[Nota Name]]} crea flashcards, estas pueden ser: Single-Line Basic: Pregunta → respuesta Single-Line Bidirectional: Info 1 ↔ Info 2 (Para estas tarjetas solo usa el simbolo ↔) Multi-line Basic: Una pregunta general |
A | La respuesta Multi-line Bidirectional: Info 1 ?? Info 2 [Context: Notes: 4 - Notas Rapidas/Agilidad.md] [Timestamp: 2026/03/11 10:31:10] |

**ai**: # Flashcards
#Mazo

## Contexto

Modelos de desarrollo de software → Describen cómo organizar el proceso de creación de un sistema
Modelos muy estructurados → Cada etapa debe completarse antes de pasar a la siguiente

^learnkit-983863643
RQ | Modelos estructurados funcionan bien cuando |
A | - Los requisitos del sistema son estables - El proyecto tiene mucho presupuesto - El tiempo de desarrollo no es crítico |

Problema de modelos estructurados → Los requisitos cambian constantemente

## Modelos de desarrollo tradicionales

^learnkit-846085656
RQ | Modelos de desarrollo tradicionales conocidos |
A | - Proceso Unificado (UP) - Modelo en V - Ciclo de Vida en Espiral |

Modelos tradicionales derivan de → Modelo en cascada

## Modelo en Cascada

Modelo en cascada → Uno de los primeros modelos de desarrollo de software
Modelo en cascada se basa en → Una secuencia lineal de etapas

^learnkit-815342508
RQ | Etapas típicas del Modelo en Cascada |
A | 1. Análisis 2. Diseño 3. Codificación 4. Pruebas 5. Operación 6. Mantenimiento |

^learnkit-138050805
RQ | Funcionamiento del Modelo en Cascada |
A | - Primero se analizan todos los requisitos. - Luego se diseña el sistema. - Después se programa. - Finalmente se prueba y se entrega. |

^learnkit-504984995
RQ | Problema del Modelo en Cascada |
A | El usuario recién puede ver o usar el sistema casi al final del proceso. Esto genera problemas porque si los requisitos cambian o algo se entendió mal, puede ser muy costoso corregirlo. |

## Proceso Unificado (UP)

Proceso Unificado (UP) → Modelo de desarrollo más organizado que el cascada, pero estructurado
Proceso Unificado (UP) se construye en partes (iteraciones) ↔ El modelo en cascada es lineal

^learnkit-971992494
RQ | Fases principales del Proceso Unificado |
A | 1. Inicio (Inception) 2. Elaboración 3. Construcción 4. Transición |

^learnkit-898306617
RQ | Características del Proceso Unificado |
A | - Se basa en casos de uso definidos por el usuario. - Tiene iteraciones, pero el proceso sigue siendo bastante planificado. - Funciona mejor cuando los requisitos no cambian demasiado. |

Problema del Proceso Unificado → Si los requisitos cambian a mitad del desarrollo, puede ser difícil adaptarse.

## Modelo en V

Modelo en V → Evolución del modelo cascada
Modelo en V se llama así porque → El proceso se representa con forma de V

Lado izquierdo del Modelo en V → Etapas de desarrollo
Lado derecho del Modelo en V → Etapas de prueba

^learnkit-670647312
RQ | Etapas de desarrollo y prueba asociadas en el Modelo en V |
A | \|Desarrollo\|Prueba\| \|---\|---\| \|Requisitos\|Prueba de aceptación\| \|Diseño del sistema\|Prueba del sistema\| \|Diseño detallado\|Prueba de integración\| \|Implementación\|Prueba unitaria\| |

^learnkit-985628864
RQ | Características del Modelo en V |
A | - Cada fase se diseña, implementa y prueba antes de pasar a la siguiente. - No tiene tanto análisis de riesgos como otros modelos. - El desarrollo sigue siendo secuencial y bastante rígido. |

## Ciclo de Vida en Espiral

Modelo espiral combina → Modelo cascada y desarrollo iterativo
Modelo espiral fue propuesto por → Barry Boehm

El proyecto en el modelo espiral se desarrolla en → Ciclos llamados espirales

^learnkit-743143158
RQ | Actividades en cada ciclo del Modelo en Espiral |
A | 1. Planificación 2. Análisis de riesgos 3. Desarrollo 4. Evaluación |

^learnkit-871283353
RQ | El Modelo en Espiral permite |
A | - Ver avances del proyecto - Identificar problemas temprano - Reducir riesgos |

## Limitaciones de los modelos tradicionales

^learnkit-198132798
RQ | Modelos tradicionales fueron útiles porque |
A | - Solo grandes empresas desarrollaban software - Los proyectos tenían presupuestos muy altos - Los requisitos cambiaban poco |

^learnkit-584509209
RQ | Problemas de los modelos tradicionales cuando |
A | - Los requisitos cambian mucho - Se necesita desarrollar rápido - El cliente quiere ver resultados tempranos |

Para resolver los problemas de los modelos tradicionales aparecen → Las metodologías ágiles

## Metodologías Ágiles

Metodologías ágiles buscan → Hacer el desarrollo más flexible

^learnkit-303965944
RQ | Objetivo de las metodologías ágiles |
A | - Reducir malentendidos - Entregar software más rápido - Adaptarse a cambios |

^learnkit-807421810
RQ | Características principales de las metodologías ágiles |
A | - Desarrollo incremental - Iteraciones cortas - Comunicación constante con el cliente - Menos documentación |

En metodologías ágiles se entregan versiones funcionales del sistema → De manera frecuente

^learnkit-712602729
RQ | Esto permite en metodologías ágiles |
A | - Detectar errores antes - Ajustar requisitos - Mejorar el producto continuamente |

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

^learnkit-998090211
RQ | Modelos tradicionales |
A | :- Rígidos - Secuenciales - Cambios costosos |

^learnkit-500904628
RQ | Metodologías ágiles |
A | :- Flexibles - Iterativas - Adaptadas a cambios [Timestamp: 2026/03/11 10:31:18] |