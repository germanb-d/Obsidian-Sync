# Notas Rapidas
La planning en un SCRUM se hacen los tickets y se distribuyen con tiempo estimado y dificultad


Abrir bd en firebase


Endpoint: una direccion en el back al cual le tiro un request


El front le va a tirar un request al back, el back debe llamar a la bd y devolver los datos en gson / json


Con el metodo poust? En el back es como el push, a traves de http con un request body y header                  el metodo htl poust.. Llega un pedazo de codigo con header y un body como imput levelNombre: juan, etc. Debo parsearlo y limpiar los datos? Tda la comunicacion es a traves de endpoints? 
Se diseña una fachada qq tendra los metodos como endpoints?


Que la comunicacion la maneje una clase distinta a parque? Tipo parque y comunicadorParque: Recibe y pasa endPoints

Estoy entendiendo como conectar el front de react con el back en java



Spring Boot para bootearlo y de compilador maven? Crea una imagen del backend como para montarlo (el bootearlo).


Usando Spring Boot y maven para el back, junto con vite y react para el front. Creame la arquitectura y el modelado que tenga una capa controlador, una capa servicios y una capa para las entidades. Todo esto para el proyecto del parque industrial usando los tps y el diagrama de clases subido como guia.

RTA de Notebook LM:

Para el desarrollo de la Plataforma de Gestión del Parque Industrial de Viedma (GPIV), se propone una arquitectura de software basada en el patrón de diseño de capas, utilizando **Spring Boot** para el backend y **React con Vite** para el frontend. Esta estructura permite una clara separación entre el modelo de dominio, la lógica de negocio y la interfaz de usuario, facilitando la mantenibilidad y escalabilidad del sistema.

---

## Respesta de Claude

Te explico todo punto por punto, como si fuera una clase ordenada:

---

**SCRUM / Planning**

En la _planning_ del sprint, el equipo toma las tareas (tickets) y les asigna dos cosas: una estimación de tiempo y un nivel de dificultad (story points). Así se decide cuánto entra en el sprint.

---

**Firebase**

Es una base de datos en la nube de Google. "Abrir BD en Firebase" significa que van a usar ese servicio como su base de datos, sin tener que instalar nada local.

---

**Endpoint**

Es una URL específica en el backend que "escucha" peticiones. Por ejemplo: `POST /api/parque/crear`. El frontend le _tira un request_ a esa dirección y el backend responde.

---

**El flujo general**

```
REACT (front)  →  request HTTP  →  JAVA (back)  →  Firebase (BD)
                                        ↓
REACT (front)  ←  JSON/GSON    ←  respuesta
```

El back recibe el pedido, consulta la base de datos, y devuelve los datos en formato **JSON** (en Java se usa la librería **GSON** para convertir objetos a JSON y viceversa).

---

**Método POST** (en tus notas dice "poust", es POST)

Es uno de los métodos HTTP. Se usa para _enviar_ datos al servidor. Cada request HTTP tiene dos partes:

- **Header**: metadatos (tipo de contenido, autenticación, etc.)
- **Body**: los datos en sí, por ejemplo `{ "nombre": "Juan", "nivel": 3 }`

Cuando llega ese request al back, vos tenés que _parsear_ el body (convertirlo de JSON a un objeto Java) y validar/limpiar los datos antes de usarlos. Sí, toda la comunicación front-back pasa por endpoints.

---

**La Fachada (Facade)**

Es un patrón de diseño. La idea es tener una clase que actúe de "intermediaria" y exponga los métodos como endpoints. En vez de que `Parque` maneje todo, separás responsabilidades:

|Clase|Responsabilidad|
|---|---|
| `Parque` |Lógica del negocio (reglas, datos)|
| `ComunicadorParque` |Recibe requests HTTP y llama a `Parque` |

Esto es exactamente lo que en Spring Boot (Java) se llama un **Controller**: una clase cuya única función es recibir requests, delegarle el trabajo a las clases de lógica, y devolver la respuesta.

---

**En resumen, la arquitectura que estás aprendiendo es:**

```
React → HTTP Request → Controller (ComunicadorParque) → Parque (lógica) → Firebase
```

Estás entendiendo los fundamentos de una arquitectura **cliente-servidor REST**, que es la más usada en la industria. ¿Querés que profundice en alguno de estos puntos?



# Arquitectura y modelo 
### 1. Arquitectura del Sistema

La solución se divide en dos grandes bloques conectados mediante una API REST:

- **Frontend (React + Vite):** Encargado de la presentación y la interacción con los diversos actores (Administración, Empresas, Organismos).
- **Backend (Spring Boot + Maven):** Organizado en tres capas principales que gestionan la persistencia, la lógica y el acceso a los datos.

---

### 2. Modelado del Backend (Spring Boot)

#### A. Capa de Entidades (Domain Layer)

Esta capa representa los objetos de negocio definidos en el **Diagrama de Clases** y el análisis de dominio. Las entidades principales incluyen:

- **Parque:** Entidad central que coordina los gestores. Atributos: `nombre`, `ubicacion`.
- **Empresa:** Representa tanto a las radicadas como a las interesadas. Atributos: `identificacion`, `actividadPrincipal`, `esRadicada`.
- **Proyecto:** Utiliza una estructura de herencia para diferenciar entre **ProyectoPreliminar** y **ProyectoDefinitivo**. Campos clave: `actividadPrincipal`, `superficieRequerida`, `estado` (ej. "En Revisión", "Aceptado").
- **Lote:** Gestiona la infraestructura física del parque. Atributos: `superficie`, `identificacion`, `estado` (disponible, reservado, vendido).
- **Usuario:** Clase base para la autenticación y roles. Subclases: `AdminParque`, `AdminEmpresa`.
- **Presupuesto e Inventario:** Entidades para el control financiero y de recursos del ENREPAVI.

#### B. Capa de Servicios (Business Logic Layer)

Aquí se implementan los procesos generales y las reglas de negocio descritas en los TPs. Los servicios actúan como una fachada para los controladores:

- **EmpresaService:** Gestiona el alta de empresas radicadas (HU 01) y el registro de nuevos interesados (HU 02).
- **ProyectoService:** Coordina la presentación de ideas, evaluación por parte de la administración (HU 05) y el seguimiento de estados. Implementa la lógica para que un proyecto preliminar aprobado permita crear uno definitivo.
- **LoteService:** Administra la disponibilidad y adjudicación de lotes (HU 07), vinculándolos a empresas tras la aprobación de proyectos.
- **PresupuestoService:** Controla las partidas presupuestarias y los gastos asociados, funcionando como un libro de estado y balances (HU 11).
- **ReporteService:** Genera estadísticas sobre ocupación, rubros y puestos de trabajo generados (HU 06).

#### C. Capa de Controladores (API REST Layer)

Define los endpoints que consume el frontend, separando las responsabilidades por perfil de usuario:

- **PublicController:** Endpoints para registro de usuarios y consulta pública de datos.
- **AdminParqueController:** Acceso a la gestión de lotes, evaluación de proyectos y generación de reportes operativos.
- **EmpresaController:** Permite a las empresas autogestionar sus proyectos, reportar consumos eléctricos y cantidad de empleados (HU 08, HU 09).

---

### 3. Modelado del Frontend (React + Vite)

La interfaz se construye mediante componentes reutilizables que consumen los servicios del backend:

- **Panel de Administración:** Tableros para el seguimiento de empresas y visualización de recursos en tiempo real.
- **Portal de Empresas:** Formularios dinámicos para la presentación de proyectos y carga de documentación técnica (PDFs para impacto ambiental, viabilidad, etc.).
- **Módulo de Inventario y Presupuesto:** Vistas tipo tabla para el control de elementos y balances financieros.

### 4. Gestión de Dependencias (Maven)

Se utiliza **Maven** para la construcción del proyecto back-end, gestionando las dependencias de **Spring Boot** (Starter Web, Data JPA, Security) y drivers de base de datos. La estructura de archivos sigue el estándar de Maven (`src/main/java` para código y `src/main/resources` para configuraciones).

Esta arquitectura de tres capas garantiza que el sistema sea capaz de centralizar la información dispersa actualmente en documentos y planillas, cumpliendo con el objetivo de optimizar la toma de decisiones en el Parque Industrial.





# Convención 

1. carpetas -> camelCase
2. archivos -> PascalCase
En java son todas las de siempre


Main





Firebise para q el sistema de usuarios sea mas sencillo. Usamos SQL 



Security: configuracion para los controladores del endpoint
- a q endpoints puede acceder q usuario
- Las comunicaciones deberian ir cifradas con JWT


Fecha de Sprint 
