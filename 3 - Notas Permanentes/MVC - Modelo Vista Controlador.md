---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# ¿Qué Es MVC?

El Modelo Vista Controlador (MVC) es un [[patrón de diseño de software]] ampliamente utilizado en diversos lenguajes de programación. De hecho, es uno de los patrones de diseño de software más populares.

MVC se compone de tres partes principales:

*   Modelo
*   Vista
*   Controlador

El objetivo principal de MVC es separar las responsabilidades dentro de una aplicación.

## Modelo

El Modelo se encarga de almacenar y administrar los datos de la aplicación. Inicialmente, puede contener los modelos de cada objeto, junto con arrays que actúan como "repositorios". Sin embargo, el objetivo final es que el Modelo se encargue exclusivamente de la conexión con la [[Base de Datos|base de datos]].

*   Representa los [[POO - Programación Orientada a Objetos#^kfgnea|objetos]] del dominio (ej: Persona, Producto, Usuario).
*   Contiene los atributos y la lógica de negocio de estos objetos.
*   Se comunica con la [[Base de Datos]] para persistir y recuperar datos.

> [!warning] A tener en cuenta
> Los modelos deben limitarse a getters, setters, el método `equals` y métodos particulares para modificar booleanos. La lógica de creación y manipulación de los objetos residirá en el Controlador.

## Vista

La Vista es la interfaz con la que el usuario interactúa. Esto incluye:

*   Pantallas
*   Formularios
*   HTML
*   Consola
*   [[Swing]]
*   JavaFX
*   Etc.

La Vista se encarga únicamente de mostrar la información al usuario.

## Controlador

El Controlador actúa como intermediario entre el Modelo y la Vista. Sus funciones principales son:

*   Recibir las acciones del usuario (clics, entradas de formulario, etc.).
*   Decidir qué acción realizar en función de la entrada del usuario.
*   Solicitar datos al Modelo.
*   Indicar a la Vista qué información debe mostrar.

El Controlador contiene la lógica de la aplicación. Por ejemplo:

**Registrar un usuario:**

1.  La Vista envía los datos necesarios para crear un usuario al Controlador, a través del método `RegistrarUsuario`.
2.  El Controlador tiene acceso al Modelo de Usuario.
3.  El Controlador, en su método `RegistrarUsuario`, toma los datos de la Vista y crea un nuevo objeto `Usuario`.
4.  El Controlador guarda el objeto `Usuario` en el array/BD.

**Obtener un Usuario:**

1.  En la Vista, se utiliza el método `ObtenerUsuario` del Controlador.
2.  El Controlador recupera el `Usuario` correspondiente de la BD o del Array.
3.  El Controlador transforma el objeto `Usuario` en un [[DTO - Data Transfer Object]].
4.  El Controlador envía el DTO a la Vista que solicitó el usuario.
