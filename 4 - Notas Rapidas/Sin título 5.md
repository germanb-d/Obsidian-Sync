# Análisis Arquitectónico De Un Sistema Java Orientado a Objetos: Justificación De la Arquitectura En Capas Y Mapeo Curricular

## I. Fundamentos Arquitectónicos: La Arquitectura En Capas Y Principios De Diseño

El diagrama de paquetes UML proporcionado define una estructura de proyecto que sigue rigurosamente el patrón de **Arquitectura en Capas (Layered Architecture)**, un diseño fundamental en la ingeniería de software empresarial, especialmente en el ecosistema [[Java]].1 Este modelo divide la aplicación en módulos horizontales, cada uno con una responsabilidad clara y con una dependencia estricta y generalmente unidireccional hacia las capas inferiores.

### I.A. Interpretación Del Diagrama: Un Modelo De Arquitectura En Capas

La estructura visualizada separa las responsabilidades del sistema en cuatro grandes componentes principales (Frontend, Backend, Entities, Commons), los cuales se traducen en cinco capas lógicas o funcionales específicas:

1. **Capa de Presentación:** Módulo `FRONTEND` (`ar.unrn.gui`). Responsable de la interacción con el usuario.
2. **Capa de Interfaz/Fachada:** Submódulo `BACKEND.[[API]]` (`ar.unrn.[[API]]`). El punto de entrada público al subsistema de negocio.
3. **Capa de Lógica de Negocio:** Submódulo `BACKEND.servicio` (`ar.unrn.servicio`). Contiene las reglas centrales del negocio.
4. **Capa de Acceso a Datos (Persistencia):** Submódulo `BACKEND.persistencia` (`ar.unrn.persistencia`). Gestiona la comunicación con la fuente de datos.
5. **Capa de Dominio/Modelo:** Módulo `ENTITIES` (`ar.unrn.modelo`). Contiene las estructuras de datos (entidades) del negocio.
6. **Capa de Infraestructura Común:** Módulo `COMMONS` (`ar.unrn.exception`). Utilidades transversales, como el manejo centralizado de errores.

El flujo de dependencia se representa mediante flechas continuas, indicando que una capa (por ejemplo, `FRONTEND`) solo conoce y utiliza los servicios proporcionados por la capa inmediatamente inferior (`BACKEND.[[API]]`). Este estricto control sobre las dependencias es clave para la salud arquitectónica del sistema.

### I.B. Justificación Del Diseño: Separación De Responsabilidades (SoC)

La razón primordial para esta división modular es el principio de **Separación de Responsabilidades (Separation of Concerns - SoC)**.3 En la informática, SoC es el principio de diseño que organiza el código base en secciones distintas, donde cada sección aborda una única preocupación o función.3

La aplicación de SoC mediante la arquitectura en capas ofrece beneficios tangibles en el desarrollo de software:

- **Mantenimiento Simplificado:** Si la tecnología de persistencia cambia (por ejemplo, de JDBC a un ORM), solo el código dentro de `ar.unrn.persistencia` debe ser modificado, sin afectar la lógica de negocio en `ar.unrn.servicio`.
- **Reutilización del Código:** Los modelos de dominio en `ENTITIES` y la lógica de negocio en `BACKEND.servicio` son agnósticos a la forma en que el sistema se presenta (GUI, Web, [[API]]). Esto permite que el _core_ del sistema pueda ser reutilizado si se desarrolla una nueva interfaz de usuario.
- **Flexibilidad en el Despliegue:** La separación permite, por ejemplo, que el `FRONTEND` y el `BACKEND` puedan ser desarrollados y desplegados de manera independiente, satisfaciendo diferentes requisitos de calidad del servicio.2

### I.C. Principios De Calidad: Cohesión Y Acoplamiento

Una arquitectura bien diseñada debe maximizar la **Cohesión** (las clases de un paquete deben estar fuertemente relacionadas y trabajar hacia un objetivo común) y minimizar el **Acoplamiento** (la dependencia entre los paquetes debe ser mínima).4

La estructura propuesta persigue un **Bajo Acoplamiento** de manera proactiva, especialmente en la dependencia crítica entre la lógica de negocio y la infraestructura de datos. Para mantener la capa de `servicio` desacoplada de los detalles específicos de la `persistencia` (como JDBC), es esencial que la comunicación se establezca a través de **[[Interfaces]]**.5 El paquete `ar.unrn.servicio` debería definir un contrato (ej., una interfaz de Repositorio) que la [[Clase]] concreta en `ar.unrn.persistencia` debe implementar.

Este enfoque asegura que el esfuerzo de mantenimiento y prueba (medido por métricas como CBO - Coupling Between Object Classes) se reduzca, ya que el servicio solo conoce la interfaz abstracta, no la implementación concreta de la [[Base de Datos]].4 Esto es un ejemplo avanzado del uso de **[[Interfaces]] y [[Polimorfismo]]** para aplicar el Principio de Inversión de Dependencias (DIP), protegiendo la lógica de negocio central de los detalles de la infraestructura.

## II. Módulos De Dominio Y Datos Compartidos (Entities Y Commons)

Estos módulos forman la base estructural del sistema, definiendo qué son los datos del negocio y cómo se manejan los errores de manera centralizada.

### II.A. Módulo ENTITIES (`ar.unrn.modelo`)

El paquete `ar.unrn.modelo` es el repositorio del **Modelo de Dominio**. Contiene las clases centrales del negocio (tales como `Alumno`, `Curso`, `Materia`). Estas clases son típicamente POJOs (Plain Old [[Java]] Objects) con atributos, constructores y métodos de acceso.

#### Aplicación De Herencia, Polimorfismo E Interfaces

En este paquete se materializan los pilares de la Orientación a Objetos. Se puede esperar ver:

- **[[Herencia]]:** Utilizada para modelar jerarquías de tipos (ej., `Persona` heredada por `Profesor` y `Estudiante`), compartiendo atributos comunes.
- **[[Polimorfismo]]:** Se manifiesta al tratar diferentes subtipos de entidades de manera uniforme o al sobreescribir métodos de la [[Clase]] padre.
- **[[Interfaces]]:** Implementadas para definir capacidades. Un ejemplo crucial es la implementación de la interfaz **Comparable** directamente en las entidades.

#### La Clase Comparable Para Ordenamiento Natural

La interfaz `[[Java]].lang.Comparable` se implementa directamente dentro de las clases de entidad (ej., `Alumno`) para establecer un **ordenamiento natural** o predeterminado.6 Esto se logra mediante la definición del método `compareTo()`. Por ejemplo, si un `Alumno` tiene un orden natural basado en su número de legajo (`id`), esa lógica reside en el método `compareTo()` de la [[Clase]] `Alumno`.

#### Elementos De la Plataforma Java En Práctica

La práctica con clases fundamentales como `String`, `System` y `LocalDate` se aplica directamente en la definición de las entidades:

- **`LocalDate`:** Se utiliza de forma nativa para manejar fechas de manera inmutable y precisa (ej., fechas de nacimiento o fechas de [[Registro]] de un evento).
- **`String`:** Se utiliza para atributos textuales.
- **`System`:** Su uso se minimiza en el modelo de dominio; las llamadas a `System.out.println` deben limitarse estrictamente a la depuración, ya que la lógica de dominio no debe estar acoplada a la salida estándar.

### II.B. Módulo COMMONS (`ar.unrn.exception`)

Este paquete está diseñado para centralizar la gestión de la infraestructura común, siendo el manejo de **[[Excepciones]]** su rol más evidente. La centralización de las [[Excepciones]] asegura que todos los módulos utilicen un vocabulario de error uniforme y de alto nivel.

#### Centralización Y Tipos De Excepciones

Aquí se definen las **[[Excepciones]] Personalizadas** del sistema. Estas se dividen en dos categorías principales 8:

1. **[[Excepciones]] Verificadas (Checked):** Extienden `Exception`. Deben ser manejadas o declaradas con `throws` en la firma del método. Se utilizan para condiciones de error que son predecibles pero recuperables (ej., intento de escribir en un [[Archivo]] bloqueado).
2. **[[Excepciones]] No Verificadas (Unchecked):** Extienden `RuntimeException`. No necesitan ser declaradas explícitamente y se utilizan para errores de programación o fallos de infraestructura no recuperables a nivel de código (ej., intento de acceder a una entidad inexistente, `EntidadNoEncontradaException`).

Un principio clave es evitar capturar `Throwable` o `Error`, ya que estos representan problemas graves e irrecuperables (como un `OutOfMemoryError`) que la aplicación no debe intentar manejar.9

#### Manejo Arquitectónico De Errores E i18n

La capa de `commons` permite aislar las capas superiores de los detalles de infraestructura. Por ejemplo, si la capa de `persistencia` encuentra una excepción técnica de bajo nivel (como una `SQLException` de JDBC), debe capturarla y relanzarla como una excepción de dominio definida en `commons` (ej., `PersistenciaException`). De esta manera, la capa `servicio` solo maneja problemas relacionados con el negocio.

Además, el manejo de **i18n (Internacionalización)** se asocia lógicamente a este paquete. Cada excepción definida en `commons` puede llevar un código de error único. Este código de error permite que la capa de presentación (`gui`) busque el mensaje de error traducido apropiado para el usuario final, manteniendo los mensajes de error textuales fuera de la lógica de negocio y del código de excepción central.

## III. El Corazón Del Sistema: Módulo BACKEND

El módulo `BACKEND` es la columna vertebral de la aplicación, implementando la lógica transaccional y el acceso a datos.

### III.A. Capa De Persistencia (`ar.unrn.persistencia`)

Esta capa es la única responsable de la interacción con el almacén de datos subyacente.

#### Uso Exclusivo De JDBC

La implementación de la conectividad a la [[Base de Datos]] a través de **JDBC ([[Java]] Database Connectivity)** reside enteramente en este paquete. Esto incluye la gestión de conexiones, la ejecución de sentencias [[SQL]] y, fundamentalmente, el mapeo de los resultados (`ResultSet`) devueltos por la [[Base de Datos]] a las **Entidades de Dominio** definidas en `ar.unrn.modelo`.

#### Desacoplamiento Tecnológico Y Principio De Inversión De Dependencias

Para proteger la arquitectura, la capa de `persistencia` no expone clases JDBC ni detalles [[SQL]]. En su lugar, implementa las [[Interfaces]] de Repositorio que fueron definidas por la capa de `servicio`.

Si bien el uso de JDBC es un detalle de implementación de infraestructura, el Principio de Inversión de Dependencias (DIP) exige que las capas superiores no dependan de los detalles concretos de las inferiores. Al implementar [[Interfaces]] definidas por el servicio, se garantiza que, si se decide migrar la tecnología de acceso a datos (por ejemplo, a un ORM como Hibernate o JPA), solo el código dentro de `ar.unrn.persistencia` necesita ser reescrito, dejando el `servicio` completamente estable. Este es un ejemplo práctico de cómo las [[Interfaces]] y el [[Polimorfismo]] facilitan la evolución tecnológica de un sistema.

### III.B. Capa De Servicios De Negocio (`ar.unrn.servicio`)

El paquete `ar.unrn.servicio` contiene la lógica de negocio central, la orquestación de operaciones complejas y la aplicación de validaciones. No debe tener conocimiento directo de la interfaz de usuario ni de los detalles de la [[Base de Datos]].

#### El Dominio De Collections, Streams Y Lambdas

Esta capa es el [[Campo]] de aplicación principal para el manejo avanzado de datos mediante las **Collections** y el [[API]] de **Stream** introducido en [[Java]] 8.

- **Collections:** Se utilizan para agrupar y manipular conjuntos de entidades recuperadas de la persistencia (ej., `List<Usuario>`).
- **Stream y Lambda:** Se emplean para procesar estas [[Colecciones]] de manera funcional y declarativa.10 Los _Streams_ no almacenan datos, sino que operan sobre una fuente de datos (como una Colección o un Array), permitiendo operaciones de filtrado, mapeo y reducción de forma encadenada.10

Las expresiones **Lambda** se utilizan como [[Interfaces]] funcionales anónimas para definir el comportamiento de las operaciones de Stream (ej., `filter(e -> e.esActivo())`), ofreciendo un código más conciso y facilitando el procesamiento secuencial y paralelo.10 Aunque las _Collections_ pueden ser reutilizadas, un _Stream_ es consumible una sola vez, lo que requiere recrearlo para una nueva travesía o procesamiento.10

#### Interfaces Comparator Y Ordenación Dinámica

Mientras que la interfaz **Comparable** define el ordenamiento natural en la entidad, la interfaz **Comparator** se utiliza en la capa de servicio para definir **múltiples órdenes personalizados** y externos a la entidad.6

Debido a que `Comparator` es una Interfaz Funcional (contiene exactamente un método abstracto, `compare(T o1, T o2)`), es el candidato perfecto para ser implementado mediante **expresiones Lambda**.6 Por ejemplo, para ordenar una lista de alumnos recuperada por el servicio por su nombre en lugar de por su legajo natural, se utilizaría un lambda: `list.stream().sorted(Comparator.comparing(Alumno::getNombre))`.

### III.C. Capa API (`ar.unrn.api`)

Este paquete sirve como el límite de acceso al _backend_. Su función principal es doble: simplificar el acceso y proteger los datos internos.

#### Implementación Del Patrón Facade

El paquete `ar.unrn.[[API]]` implementa el patrón **[[Facade]] (Fachada)**.12 Este patrón estructural proporciona una interfaz simplificada y unificada al subsistema complejo que se encuentra debajo (es decir, la interacción entre `servicio` y `persistencia`).12

El [[Facade]] oculta la complejidad de las operaciones internas de negocio y transaccionales del `servicio`, exponiendo solo los métodos que la capa de presentación (`gui`) necesita. Esto asegura que la capa de presentación no tenga conocimiento de la orquestación de múltiples servicios o repositorios requerida para una sola operación de negocio.13

#### Aplicación Del Patrón DTO (Data Transfer Object)

La capa [[API]] es el punto donde se utiliza el patrón **DTO (Data Transfer Object)**. Los DTOs son objetos que llevan datos entre procesos o capas para reducir el número de llamadas a métodos.14 Son POJOs planos que contienen solo datos y accesores, sin lógica de negocio.14

El uso de DTOs en la [[API]] es fundamental y cumple dos objetivos arquitectónicos clave:

1. **Seguridad y Aislamiento:** La [[API]] mapea las **Entidades de Dominio** (que contienen todos los datos, incluyendo potencialmente información sensible) devueltas por el servicio a los **DTOs**. Solo el DTO, que puede contener un subconjunto seguro e insensible de los campos de la entidad, es serializado y enviado a la capa de presentación.15 Esto evita exponer la estructura completa del modelo de dominio o datos confidenciales.
2. **Optimización y Flexibilidad:** Permite a la [[API]] construir vistas de datos optimizadas para las necesidades específicas del cliente (la `gui`), incluso combinando datos de múltiples entidades en un solo DTO para reducir la necesidad de múltiples solicitudes.14

## IV. La Capa De Presentación Y la Interacción Final

### IV.A. Módulo FRONTEND (`ar.unrn.gui`)

El paquete `ar.unrn.gui` es la capa de **Presentación**, donde se construye la interfaz de usuario. Esta capa interactúa **exclusivamente** con el `ar.unrn.[[API]]` (el [[Facade]]) para realizar operaciones, consumiendo y mostrando los DTOs.

#### AWT vs. Swing En Java

La creación de GUIs en [[Java]] se realiza típicamente utilizando **[[AWT]] (Abstract Window Toolkit)** o **[[Swing]]**.

- **[[AWT]]:** Los componentes de [[AWT]] son _heavyweight_ (dependientes del sistema operativo), lo que significa que su apariencia es nativa del SO. Es más eficiente y rápido para componentes básicos, pero su conjunto de componentes es más limitado.16
- **[[Swing]]:** Los componentes de [[Swing]] son _lightweight_ (dibujados por [[Java]]), lo que garantiza una apariencia consistente y plataforma-independiente. [[Swing]] ofrece un conjunto de componentes más rico (tablas, árboles, _sliders_) y, fundamentalmente, soporta el patrón Modelo-Vista-Controlador (MVC), lo que es ideal para aplicaciones complejas.16

Dada la naturaleza avanzada del curso de OOP 2, es altamente probable que el paquete `ar.unrn.gui` esté implementado usando **[[Swing]]**, aprovechando su flexibilidad y su capacidad para construir [[Interfaces]] ricas y consistentes, además de facilitar la implementación del patrón MVC para mantener la lógica de la vista separada del controlador.

### IV.B. La Plataforma Java

El proyecto se sustenta en la **Plataforma [[Java]]**, que garantiza un entorno de ejecución coherente y robusto para todos los módulos, desde las clases de dominio inmutables como `LocalDate` hasta la conectividad con JDBC y la construcción de la interfaz gráfica con [[Swing]]. La Máquina Virtual de [[Java]] (JVM) proporciona la capa de abstracción necesaria para que el sistema funcione de manera efectiva en cualquier entorno que cumpla con el estándar [[Java]].

## V. Resumen De Mapeo Curricular Y Estructura Arquitectónica

La división del proyecto en paquetes, como se ilustra en el diagrama, no es una convención de nomenclatura, sino una manifestación práctica de los principios de la ingeniería de software aprendidos en un contexto de Programación Orientada a Objetos 2. La justificación de la arquitectura es la necesidad de conseguir **mantenibilidad, escalabilidad y flexibilidad** a través de la Separación de Responsabilidades.

El análisis de la estructura permite identificar dónde se aplican los conceptos académicos avanzados de [[Java]], proporcionando una hoja de ruta clara para el estudio y la implementación.

### V.A. Mapeo De Componentes Y Conceptos Clave

A continuación, se presenta una tabla que resume la función arquitectónica de cada componente y cómo los temas curriculares se aplican directamente en esa capa.

Tabla de Mapeo Curricular y Componentes Arquitectónicos

|**Tópico de la Asignatura**|**Ubicación Principal Sugerida**|**Detalle de la Aplicación Práctica**|
|---|---|---|
|[[Herencia]], [[Polimorfismo]], [[Interfaces]]|`modelo`, `servicio`, `persistencia`|[[Interfaces]] de Repositorio (DIP) en Persistencia. Jerarquías de clases en el Modelo de Dominio.|
|[[Facade]], DTOs|`[[API]]`, `gui`|`[[Facade]]` simplifica el acceso en `[[API]]`. DTOs aseguran transferencia de datos seguros y optimizados entre `servicio`/`[[API]]`/`gui`.|
|JDBC|`persistencia`|Conectividad, ejecución de [[SQL]], y mapeo de `ResultSet` a Entidades. Aislado de otras capas.|
|Collections, Stream, Lambda|`servicio`|`Collections` para manejo interno de datos. `Stream` y `Lambda` para procesamiento funcional eficiente, filtros y transformaciones declarativas.|
|Exceptions + i18n|`commons`|Definición de [[Excepciones]] de negocio (Verificadas/No Verificadas) y centralización de códigos de error para traducción.|
|Comparable/Comparator|`modelo`, `servicio`|`Comparable` para orden natural en Entidades; `Comparator` (como Lambda) para ordenación externa y dinámica en el servicio.|
|[[AWT]] / [[Swing]]|`gui`|Creación de la interfaz gráfica de usuario. Se recomienda [[Swing]] por su soporte a MVC y componentes enriquecidos.|
|La [[Clase]] String, System y LocalDate|`modelo` (Principal)|Uso de `LocalDate` para manejo de fechas inmutable, y gestión de atributos `String` en POJOs.|

### V.B. Conclusiones Arquitectónicas

La estructura del proyecto de [[Java]] presentado es un modelo canónico de **Layered Architecture** impulsado por el principio de **Separación de Responsabilidades**.

La división en capas establece una cadena de causa y efecto:

1. **Separación de Responsabilidades:** Requiere que las capas interactúen de manera controlada.
2. **Bajo Acoplamiento:** Esta necesidad obliga al uso obligatorio de **[[Interfaces]] y [[Polimorfismo]]** en las fronteras, especialmente para aislar el `servicio` de la `persistencia` (aplicando DIP).
3. **Seguridad y Usabilidad:** La interfaz de acceso al negocio debe ser simple y segura, lo que se resuelve mediante la aplicación del patrón **[[Facade]]** en el paquete `[[API]]` y el uso de **DTOs** para proteger la integridad y estructura del modelo de dominio interno.

En resumen, la división del [[Archivo]] ZIP de [[Java]] no es una elección estética, sino una implementación estratégica de los principios avanzados de la Orientación a Objetos y de la arquitectura de software, diseñada para generar un sistema robusto, flexible y fácilmente mantenible. El conocimiento y la aplicación correcta de estos patrones demuestran la transición de la programación orientada a objetos básica al desarrollo de sistemas empresariales.
