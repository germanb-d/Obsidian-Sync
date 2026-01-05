---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Concepto Principal

![[Facade-1759374376002.webp]]

Simplifica el uso de un sistema complejo al ofrecer una **interfaz unificada de alto nivel** para acceder a sus diversos subsistemas.

## Beneficios Clave

- Reduce las dependencias entre el cliente y los subsistemas.
- Oculta la complejidad interna del sistema.
- Facilita el uso general del sistema.

# Estructura

1.  **Cliente**: Accede únicamente al [[Facade]].
2.  **[[Facade]]**: Expone operaciones de alto nivel que delegan las llamadas a los subsistemas correspondientes.
3.  **Subsistemas**: Contienen la lógica de negocio y la funcionalidad interna.

# Ejemplo Práctico

Encender un teléfono es un buen ejemplo. Internamente, este proceso involucra la CPU, la batería, el GPS y el WiFi. Sin embargo, el cliente (usuario) solo interactúa con un método simple como `facade.on()`, sin necesidad de conocer la complejidad subyacente.

# Relación Con Otras Arquitecturas

Aunque el [[Facade]] puede emplear internamente una arquitectura [[MVC - Modelo Vista Controlador]] (debido a la presencia de vistas, modelos y métodos), conceptualmente funciona como una capa de acceso o interfaz de usuario dentro de un sistema más amplio.

El [[Facade]] se comunica con otras capas utilizando exclusivamente objetos [[DTO - Data Transfer Object]]. Estos DTOs transfieren datos sin exponer la lógica interna de los métodos. El flujo es el siguiente: los métodos reciben el DTO, lo convierten al modelo real, ejecutan su función y devuelven otro DTO. Esto mantiene al [[Facade]] desacoplado de la implementación y estructura de los modelos lógicos.

#Revisar
