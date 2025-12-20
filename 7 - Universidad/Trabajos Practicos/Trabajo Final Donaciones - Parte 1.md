# Tarjetas CRC

---

| Clase                 | Persona                                                                                          |
| --------------------- | ------------------------------------------------------------------------------------------------ |
| **Responsabilidades** | - Mantener información personal básica (nombre, apellido, DNI). <br>- Imprimir datos personales. |
| **Colaboradores**     | - Donante <br>- Voluntario                                                                       |

---

| Clase                 | Donante                                                                                                                                   |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Heredar información personal de Persona. <br>- Mantener información de ubicación/dirección. <br>- Imprimir datos completos del donante. |
| **Colaboradores**     | - Persona <br>- Ubicación <br>- PedidoDonacion <br>- Organización                                                                         |

---

| Clase                 | Voluntario                                                                      |
| --------------------- | ------------------------------------------------------------------------------- |
| **Responsabilidades** | - Heredar información personal de Persona. <br>- Imprimir datos del voluntario. |
| **Colaboradores**     | - Persona <br>- OrdenDeRetiro <br>- Organización                                |

---

| Clase                 | Ubicación                                                                                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Mantener datos de dirección (calle, número, zona, barrio). <br>- Mantener coordenadas geográficas (ejeX, ejeY). <br>- Imprimir información de ubicación. |
| **Colaboradores**     | - Donante                                                                                                                                                  |

---

| Clase                 | PedidoDonacion                                                                                                                                                                                                                                       |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Registrar información del donante solicitante. <br>- Mantener fecha de emisión del pedido. <br>- Especificar bienes a donar. <br>- Indicar disponibilidad de vehículo. <br>- Registrar observaciones adicionales. <br>- Imprimir datos del pedido. |
| **Colaboradores**     | - Donante <br>- OrdenDeRetiro <br>- Organización                                                                                                                                                                                                     |

---

| Clase                 | OrdenDeRetiro                                                                                                                                                                                                                                                                      |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Gestionar estados de la orden (PENDIENTE, EJECUCION, COMPLETADO). <br>- Mantener fecha de emisión. <br>- Asociar pedido de donación correspondiente. <br>- Ejecutar y completar órdenes. <br>- Gestionar visitas asociadas (agregar/eliminar). <br>- Imprimir datos de la orden. |
| **Colaboradores**     | - PedidoDonacion <br>- Voluntario <br>- Visita <br>- Organización                                                                                                                                                                                                                  |

---

| Clase                 | Visita                                                                                                                  |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Registrar fecha de la visita. <br>- Mantener observaciones de la visita. <br>- Gestionar bienes donados en la visita. |
| **Colaboradores**     | - OrdenDeRetiro <br>- BienDonado                                                                                        |

---

| Clase                 | BienDonado                                                                                                            |
| --------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Clasificar bienes por categoría (ALIMENTO, ROPA, MOBILIARIO, HIGIENE, OTROS). <br>- Asignar puntaje al bien donado. |
| **Colaboradores**     | - Visita                                                                                                              |

---

| Clase                 | Organización                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Responsabilidades** | - Mantener nombre de la organización. <br>- Gestionar registro de donantes (registrar, eliminar, imprimir). <br>- Gestionar registro de voluntarios (registrar, eliminar, imprimir). <br>- Gestionar pedidos de donación (registrar, eliminar, imprimir). <br>- Gestionar órdenes de retiro (registrar, eliminar, imprimir). <br>- Verificar existencia de personas por DNI. |
| **Colaboradores**     | - Donante <br>- Voluntario <br>- PedidoDonacion <br>- OrdenDeRetiro                                                                                                                                                                                                                                                                                                          |

---

# UML

![[Sin títul![[Obsidian-Sync/1 - Archivos Adjuntos/Diagramas/Trabajo Final Donaciones - Parte1.svg]]o 4.svg]]
