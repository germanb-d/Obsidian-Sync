---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Capas Arquitectónicas

![[Capas Arquitectónicas-1759371564460.webp]]

Las capas arquitectónicas dividen un sistema en distintos niveles de responsabilidad.  
El objetivo es **separar responsabilidades**, mejorar la mantenibilidad y hacer que el sistema sea más escalable.

- **Presentación / UI** → maneja la interacción con el usuario (ventanas, formularios, páginas web).
- **Aplicación / Dominio** → contiene las reglas de negocio y las entidades (ejemplo: Usuario, Pedido, Rol).
- **Persistencia / Infraestructura** → maneja el acceso a datos y servicios externos (base de datos, repositorios, APIs).

Cada capa conoce solo lo necesario de la capa inmediatamente inferior. Por ejemplo, la capa de UI no debería conocer cómo funciona la base de datos, solo recibe datos listos para mostrar.

Lo podemos ver como quel las **capas arquitectónicas** son una subdivisión interna de una [[arquitectura]], para detallar mejor cómo se estructuran y conectan los componentes.

---

# Diferencia Con MVC

El patrón [[MVC - Modelo Vista Controlador]] no organiza todo el sistema, sino que se aplica principalmente dentro de la **capa de Presentación**.  
Su propósito es estructurar cómo se comunican la interfaz de usuario y la lógica de negocio:

- **Modelo (M)** → contiene los datos y reglas de negocio relevantes para la UI.
- **Vista (V)** → muestra los datos al usuario.
- **Controlador (C)** → recibe las acciones del usuario, coordina con el Modelo y actualiza la Vista.

Mientras que las **capas arquitectónicas** organizan el sistema completo, el **MVC** organiza la interacción en la interfaz de usuario.

---

# Ejemplo De Aplicación De MVC Dentro De Las Capas

En una arquitectura por capas, la estructura se vería así:

```
Arquitectura en Capas (visión global)
-------------------------------------
[ Capa de Presentación ]
     └─ aquí vive MVC
        - Vista
        - Controlador (puede implementarse como un Facade)
        - Modelo (DTO o dominio simplificado para la UI)

[ Capa de Lógica / Dominio ]
     └─ Reglas de negocio, entidades ricas, casos de uso

[ Capa de Persistencia ]
     └─ Acceso a base de datos, repositorios, APIs externas
```

De esta forma:

- La **capa de Presentación** utiliza MVC para separar Vista, Controlador y Modelo. Junto con patrones como el [[Facade]].
- El **Modelo en MVC** puede apoyarse en [[DTO - Data Transfer Object]] o clases de dominio simplificadas para que la UI no dependa de toda la complejidad interna.
- El **Controlador en MVC** puede servirse de un **Facade** para comunicarse con la lógica de aplicación sin exponer la complejidad al usuario.

#Completar

## Arquitecuta Armada

Frontend

- Todos los DTOs.
Backend
- Api: el FACADE
- Servicio: para crear servicios para resolver algo como entrar con cuenta de Google (algo q no usamos aún)
- Persistencia: En principio solo en la memoria posteriormente en una base de datos¿ el main?
Entities
- Las entidades que creemos como usuario, donante, etc
Commons
- Aun no lo vimos
- Seria algo donde guardaremos lo comun entre todos los paquetes
