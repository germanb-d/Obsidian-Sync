---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Parcial
  - Teoria
---

Preguntas exactas para coloquio:

1. *¿Qué es un archivo en el contexto de bases de datos y cómo se diferencia de otras estructuras de datos?*
2. *¿Qué diferencias hay entre un archivo lógico y un archivo físico?*
3. *¿Qué es un bloque en un archivo? ¿Qué función cumple respecto a los registros que contiene?*
4. **¿Qué ventajas ofrece agrupar registros en bloques en lugar de almacenarlos de forma secuencial simple?**
5. *¿Cómo se administra el espacio en archivos con registros de longitud variable?*
6. *¿Qué es la fragmentación interna y externa en archivos? ¿Cómo puede evitarse o corregirse?*
7. *¿Qué diferencias hay entre baja lógica y baja física de un registro? ¿Cuándo se recomienda cada una?*
8. *¿Qué estrategias existen para recuperar el espacio ocupado por registros eliminados?*
9. *¿Cómo influye el diseño físico de un archivo en el rendimiento del acceso a los datos?*

# 🔍 *Índices*

10. *¿Qué es un índice en una base de datos y cuál es su propósito principal?*
11. *¿Cuál es la diferencia entre un índice primario y uno secundario?*
12. *¿Qué ventajas tiene el uso de índices? ¿Qué desventajas puede haber?*
13. *¿Qué significa que un índice sea “selectivo”? ¿Por qué es importante?*
14. *¿Qué operaciones requieren actualización del índice?*
15. *¿Qué estrategias existen para manejar múltiples índices en un archivo con muchas búsquedas diferentes?*

---

# 🌳 *Árboles E Índices jerárquicos*

16. *¿Qué problema resuelven los árboles en el contexto de archivos e índices?*
17. *¿Cuál es la principal diferencia entre un árbol binario y un árbol B?*
18. *¿Qué ventajas tiene usar un árbol B o B+ frente a un árbol binario simple?*
19. *¿Qué es la “paginación” en árboles y qué relación tiene con los bloques de archivos?*
20. *¿Por qué se dice que los árboles B+ son ideales para acceso secuencial e indexado al mismo tiempo?*
21. *¿Cómo se realiza una inserción o eliminación eficiente en un árbol B?*
22. *¿Qué significa que un árbol esté “balanceado” y por qué es importante?*

---

# 🎯 *Preguntas integradoras*

23. *¿Cómo se combinan los conceptos de archivos, bloques, índices y árboles para lograr eficiencia en bases de datos grandes?*
24. *¿Qué decisiones debe tomar un diseñador de base de datos al elegir entre almacenamiento secuencial, indexado o por dispersión (hashing)?*
25. *¿Cómo influye el tamaño de bloque en el rendimiento general del sistema de almacenamiento?*

Preguntas generales para coloquio (nivel comprensión):

1. *¿Cuál sería la mejor forma de aprovechar el espacio en archivos de base de datos?*
2. *¿Qué estrategia usarías para que una base de datos con muchos registros pueda mantenerse ordenada y rápida al buscar datos?*
3. *¿Qué problemas puede traer eliminar registros en un archivo, y cómo se puede solucionar?*
4. *¿Por qué no conviene guardar registros de longitud variable sin ningún tipo de control?*
5. *¿Qué ventajas tiene utilizar un índice en un archivo? ¿Y qué posibles desventajas?*
6. *Si tuvieras que diseñar un sistema que consulte mucha información ordenada, ¿qué tipo de estructura elegirías y por qué?*
7. *¿Qué papel juegan los bloques en el aprovechamiento del espacio y el rendimiento del acceso a los datos?*
8. *¿Qué estrategia de organización de archivos te parece más eficiente: secuencial, directo o indizado? ¿Por qué?*
9. *¿Por qué es importante que las hojas de un árbol B estén todas al mismo nivel?*
10. *¿Qué sucede si no se controla el crecimiento del archivo y no se reorganiza nunca?*

Registros de longitud fija vs variable

Bajas logicas vs bajas fisicas

Aprovechar las bajas logicas para nuevas altas

Como se lleva la cuenta de los espacios disponibles en registros de longitud fija y

Variable

Que es la fragmentación interna y externa

Que tipo de fragmentación se puede dar en registros de longitud fija, y variable

Como se lidia con la fragmentacion interna y externa.

Que es un indice primario y para que sirve

Que es un indice secundario y para que sirve

Como esta compuesto un indice primario y como se utiliza

Como esta compuesto un indice secundario y como funciona

Que es un indice selectivo

Que pasa si un indice es demasiado grande

Como se realizan las operaciones (baja, alta, modificacion) sobre indices primarios y

Secundarios

Para que sirve el flag del indice
